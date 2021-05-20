# django , ajax , file_upload

파일 업로드 즉시 업로드 하는게 아닌 저장 버튼을 눌렀을 때 수동으로 업로드 할 수 있는 코드

- jquery
```
function file_save() {

      var file = $("#orgLicenseFile")[0].files[0];
      var filename = file.name;
      var filetype = file.type.split('/')[1];
      var reader = new FileReader();

      $("#filename").val(filename);
      reader.onload = function (e) {
          // 변환이 끝나면 reader.result로 옵니다.
          var base64data = reader.result;
          // 여기서 구조가 중요합니다.
          // 구조는 「data: 파일 타입; base64, 데이터」입니다.
          var data = base64data.split(',')[1];
          //data가 이제 데이터 입니다.
          //사실 ajax로 넘길때는 큰 사이즈 설정해서 데이터를 넘기면 빠르게 되는데
          //예제이다보니 프로그래스바 구조를 나타내기 위해 문자 1개 단위로 보내겠습니다.
          var sendsize = 5096;
          var filelength = data.length;
          var pos = 0;

          console.log(data)
          console.log(filetype)

          $.ajax({
              type: 'POST',
              dataType: 'json',
              data: {
                  data: data,
                  filetype: filetype,
                  csrfmiddlewaretoken : $.cookie('csrftoken'),
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
