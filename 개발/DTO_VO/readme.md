# DTO VS VO

# DTO(Data Transfer Object)

계층(Layer) 간 데이터 교환을 위한 객체

### 특징

1. DTO는 데이터 접근 메서드 외의 기능을 가지지 않는다 
2. 값을 유연하게 변경 가능
3. 주로 API 데이터를 반환하거니 읽기 모델에서 사용

```java
public class RegisterDTO{
	private String id, title, content, author;
	public RegisterDTO(String id, String title, String content, String author) {
			super();
			this.id = id;
			this.title = title;
			this.content = content;
			this.author = author;
		}
	
		public String getId() {
			return id;
		}
	
		public void setId(String id) {
			this.id = id;
		}
	
		public String getTitle() {
			return title;
		}
	
		public void setTitle(String title) {
			this.title = title;
		}
	
		public String getContent() {
			return content;
		}
	
		public void setContent(String content) {
			this.content = content;
		}
	
		public String getAuthor() {
			return author;
		}
	
		public void setAuthor(String author) {
			this.author = author;
		}
	
}
```

getter, setter 메서드 외에 비즈니스 로직을 가지지 않음

# VO(Value Object)

값을 가지는 객체

### 특징

1. 변하지 않는 값을 가지는 객체 → 값이 변하지 않음을 보장하며 코드의 안정성과 생산성 높임
2. 값이 같다면 동일한 객체임 (equals() 와 hashCode() 메서드를 오버라이드하여 객체 비교)

```java
public class RegisterVO{
	private String id, title, content, author;
	@Override
	public boolean equals(Object o){
		if (this==o) return true;
			if (o == nul || getClass() != o.getClass()) return false;
			RegisterVO regVo = (RegisterVO) o;
			return Objects.equals(id.regVo.id) && Objects.equals(title, regVo.title) && 
			Objects.equals(content, regVo.content) && Objects.equals(author, regVo.author);
	}
	@Override
	public int hashCode(){
		return Objects.hash(id,title,content,author);
	}
}
```

equals() 와 hashCode()가 재정의 되어 객체의 값 자체를 비교

VO 역시 getter 와 setter을 가질 수 있다.

## 공통점

레이어 간 데이터를 전달할 때 사용 가능함 

## 차이점

[DTO VS VO](https://www.notion.so/ed2a9441f34c41cfa177f9a58b900b13)

JPA에서는 VO와 DTO를 정확히 구분지어 사용하지만, MyBatis를 사용하고 있다면 대부분 VO 또는 DTO 한개를 사용. 

---

Reference

[https://parkadd.tistory.com/53](https://parkadd.tistory.com/53)

[https://webdevtechblog.com/entity-vo-dto-666bc72614bb](https://webdevtechblog.com/entity-vo-dto-666bc72614bb)
