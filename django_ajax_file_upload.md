# django , ajax , file_upload

파일 업로드 즉시 업로드 하는게 아닌 저장 버튼을 눌렀을 때 수동으로 업로드 할 수 있는 코드

- jquery
```
function file_save() {

var file = $("#orgLicenseFile")[0].files[0];
var filename = file.name;
var filetype = file.type.split('/')[1];

console.log(file)
var reader = new FileReader();

$("#filename").val(filename);

reader.readAsDataURL(file)

reader.onload = function (e) {
    // 변환이 끝나면 reader.result로 옵니다.
    var base64data = reader.result;
    var data = base64data.split(',')[1];

    console.log(data)
    console.log(filetype)

    $.ajax({
        type: 'POST',
        dataType: 'json',
        data: {
            data: data,
            filetype: filetype,
            csrfmiddlewaretoken: $.cookie('csrftoken'),
        },
        url: '{% url "file_upload" %}',
        success: function (data) {

        },
        error: function (jqXHR, textStatus, errorThrown) {
        },
        complete: function (jqXHR, textStatus) {
        }
    });
};
}
```

> html input file type 의 input 을 만들어 업로드 한다. 저장 이라는 버튼을 클릭하였을때 file을 읽어
> base64 로 encoding한 후 그 text를 서버 (backend, django) 로 보내준다.

- django
```
def file_upload(request):

    path = MEDIA_URL

    # filename =

    data = request.POST.get('data')

    data_decode = base64.b64decode(data)

    file_name = 'test'

    save_path = path + file_name + "." + request.POST.get('filetype')

    with open(save_path, 'wb') as f:
        f.write(data_decode)
```

> django 에서는 base64의 값을 받은 후, decode한 뒤 저장 경로에 맞춰 저장하여 준다. 



>> 이후 처리에는 db저장 부분이 있는데 그건 알아서 맞춰서 해주도록 
