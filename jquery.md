# juqery

### form에 script을 사용해 유동적으로 추가하는법

```
$("#form").append($("<input>", {
    type: "hidden",
    id: "course_id",
    name: "course_id",
    value: v.course_id
}));
```
