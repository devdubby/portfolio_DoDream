# 신한 두드림 직무교육(4주)

1주차 : 협업 및 프로젝트 관리를 위한 Git/Github의 이해
2주차 : Firebase의 이해와 기능 활용
3주차 : Firebase를 활용한 웹 채팅 구현
4주차 : Jasmine을 활용한 TDD 로또 프로그램 구현

## 1주차 교육 - git 명령어
$ git init
해당 폴더에 git을 활성화 시킨다.

###

$ git remote add [remote 이름] [remote 주소]
ex) git remote add origin https://github.com/seong954t/DoDreamEdu.git
github주소를 연동할 수 있게 해준다.

###

$ git add [. / * / 파일이름]
ex) git add README.md
저장소에 올릴 수정된 파일을 알려준다.

###

$ git commit -m "변경사항에 대한 커밋 내용"
ex) git commit -m "modify readme.md file"
add한 내용에 대해 코멘트를 작성한다.

###

$ git push [remote 이름] [branch 이름]
ex) git push origin master
add와 commit 후 변경 내용에 대해 github 저장소에 업로드한다.
 
###

$ git branch [branch 이름]
ex) git branch addName
필요한 기능을 다른 branch와 별도로 작업하기 위해 새로운 branch를 생성한다.

###

$ git branch
현재 branch의 목록을 확인할 수 있다.

###

$ git branch -D [branch 이름]
ex) git branch -D addName
해당 branch를 삭제한다.

###

$ git checkout [branch 이름]
ex) git checkout addName
현재 branch에서 자신이 작업하고자하는 branch로 이동한다.

###

$ git fetch [remote 이름]
ex) git fetch origin
해당 remote에 있는 내용을 로컬로 가져온다.
 
###

$ git merge [remote 이름]/[branch 이름]
ex) git merge origin/master
fetch된 내역들을 해당 remote의 branch로 병합을 한다.

###

$ git pull [remote 이름] [branch 이름]
ex) git pull origin master
github의 변경사항을 현재 로컬에 동기화한다. fetch+merge와 동일한 일을 수행한다.

## 2주차 교육 : JQuery, FireBase

## JQuery

### class, id 접근하기

$(".클래스 이름")
$("#아이디 이름")

### input 값 가져오기 or 넣기

$("#아이디 이름").val()

    ex) $("#email-input").val()

$("#아이디 이름").val("입력할 내용")

    ex) $("#email-input").val("myname@github.com")

### text 내용 가져오기 or 넣기

$("#아이디 이름").text()

    ex) $("#title").text()

$("#아이디 이름").text("입력할 내용")

    ex) $("#title").text("타이틀 입니다.")

  
### 클릭 이벤트 설정하기

$("#아이디 이름").click( 함수 )

    ex) $("#btn").click(function() {
		    alert("클릭 이벤트")
	    });

### class 이름 추가 or 제거하기

$("#아이디 이름").addClass("클래스 이름")

    ex) $("#login-btn").addClass("enable-login")

$("#아이디 이름").removeClass("클래스 이름")

    ex) $("#login-btn").removeClass("disable-login")

  
### DOM 보이기 or 숨기기

$("아이디 이름").show()

    ex) $("#login-err").show()

$("아이디 이름").hide()

    ex) $("#login-err").hide()

### 키보드 이벤트 설정하기

$("#아이디 이름").keyup( 함수 )

    ex) $("#email-input").keyup(function(event){
		    console.log(event.keyCode)
	    });

$("#아이디 이름").keypress( 함수 )

    ex) $("#email-input").keypress(function(event){
		    console.log(event.keyCode)
	    });

## FIREBASE

### 로그인 상태 변화 감지

    firebase.auth().onAuthStateChanged(function (user) {
	    if (user) {
		    로그인 상태 or 변경될 경우 실행된다.
	    } else {
		    로그인 상태가 아닌 경우 or 로그아웃할 경우 실행된다.
		}
	});

### 회원가입

    firebase.auth().createUserWithEmailAndPassword(사용자 이메일, 사용자 비밀번호)
    .then(
	    function(user){
		    기존 회원가입이 없는 최초 회원가입일 경우 진행된다.
	    },
	    function(error){
		    if(error.code == "auth/email-already-in-use"){
			    이미 해당 회원이 있는 경우 진행된다.
		    } 
		    else if(error.code == "auth/invalid-email"){
			    사용불가능한 이메일일 경우 진행된다.
		    } 
		    else if(error.code == "auth/weak-password"){
			    사용불가능한 비밀번호일 경우 진행된다.
		    } 
		    else{
			    이 외의 경우 추가적으로 있음
		    }
	    }
    )

  

### 로그인

    firebase.auth().signInWithEmailAndPassword(사용자 이메일, 사용자 비밀번호)
    .then(
	    function(user) {
		    로그인이 성공한 경우 진행된다.
	    },
	    function(error) {
		    if(error.code == "auth/user-not-found"){
			    등록된 회원이 없을 경우 진행된다.
		    }
		    else if(error.code == "auth/invalid-email"){
			    사용불가능한 이메일일 경우 진행된다.
		    }
		    else if(error.code == "auth/wrong-password"){
			    비밀번호가 올바르지 않은 경우 진행된다.
		    } 
		    else {
			    이 외의 경우 추가적으로 있음
			}
	    }
    );

### 로그인 정보 가져오기

  

사용자 UID

firebase.auth().getUid()

firebase.auth().currentUser.uid


사용자 EMAIL

firebase.auth().currentUser.email

  

### 데이터 베이스 추가하기


firebase.database().ref(데이터 베이스 경로).set( 추가할 데이터 );


firebase.database().ref(데이터 베이스 경로).update( 업데이트할 데이터 );

  

데이터 베이스 경로 - String

"user/email/name"

과 같은 "/" 로 구분한 경로

  

추가 및 업데이트할 데이터 - Object

{
$~~$key1 : value1,
$~~$key2 : value2,
$~~$key3 : value3
}

와 같은 형식의 데이터

  

#### 데이터 베이스 이벤트 받아오기

  

firebase.database().ref(데이터 베이스 경로).on(이벤트 이름, 함수)

- child_added 
항목 목록을 검색하거나 항목 목록에 대한 추가를 수신 대기합니다.
이 이벤트는 기존 하위 항목마다 한 번씩 발생한 후 지정된 경로에 하위 항목이 새로 추가될 때마다 다시 발생합니다.
리스너에는 새 하위 항목의 데이터를 포함하는 스냅샷이 전달됩니다.

- child_changed 
목록의 항목에 대한 변경을 수신 대기합니다.
이 이벤트는 하위 노드가 수정될 때마다 발생합니다.
여기에는 하위 노드의 하위에 대한 수정이 포함됩니다.
이벤트 리스너에 전달되는 스냅샷에는 하위 항목의 업데이트된 데이터가 포함됩니다.

- child_removed 
목록의 항목 삭제를 수신 대기합니다.
이 이벤트는 바로 아래 하위 항목이 삭제될 때 발생합니다.
콜백 블록에 전달되는 스냅샷에는 삭제된 하위 항목의 데이터가 포함됩니다.

- child_moved 
순서 있는 목록의 항목 순서 변경을 수신 대기합니다.
현재의 정렬 기준에 따라 항목 순서 변경의 원인이 된 child_moved 이벤트가 
child_changed 이벤트를 항상 뒤따릅니다.

- 데이터 정렬
orderByChild() 지정된 하위 키 또는 중첩된 하위 경로의 값에 따라 결과를 정렬합니다.
orderByKey() 하위 키에 따라 결과를 정렬합니다.
orderByValue() 하위 값에 따라 결과를 정렬합니다.

- 데이터 필터링
limitToFirst() 정렬된 결과 목록에서 맨 처음부터 반환할 최대 항목 개수를 설정합니다.
limitToLast() 정렬된 결과 목록에서 맨 끝부터 반환할 최대 항목 개수를 설정합니다.
startAt() 선택한 정렬 기준 메소드에 따라 지정된 키 또는 값보다 크거나 같은 항목을 반환합니다.
endAt() 선택한 정렬 기준 메소드에 따라 지정된 키 또는 값보다 작거나 같은 항목을 반환합니다.
equalTo() 선택한 정렬 기준 메소드에 따라 지정된 키 또는 값과 동일한 항목을 반환합니다.

-

    ex)firebase.database().ref('UsersConnection/').orderByChild("connection").equalto(true)
    .once(
	    'value',
	    function(snapshot){
		    snapshot.forEach(function(childSnapshot) {
			    var childKey = childSnapshot.key;
			    var childData = childSnapshot.val();
		    });
	    },
	    function(error){
	    
	    }
	)
    
    ex)firebase.database().ref('UsersConnection/')
    .on(
	    'child_added',
	    function(snapshot){
		    console.log(snapshot.key, snapshot.val())
	    },
	    function(error){
		    console.log(error);
	    }
    )

## 3주차 교육 : Firebase를 활용한 웹 채팅 구현

- 로그인 화면
> 이메일, 비밀번호 입력 시 로그인
> 가입된 이메일이 없을 시 자동 회원가입 -> 로그인

![enter image description here](https://user-images.githubusercontent.com/35620465/44072779-ab074f26-9fcb-11e8-8889-57c6eada8ef2.jpg)

- 채팅 화면
> 수정 버튼 클릭 시 닉네임 변경 가능
> 채팅에 접속한 인원수에 따라 사람아이콘 옆 인원수 숫자 표시
> 빨간색 버튼 클릭 시 로그아웃

![enter image description here](https://user-images.githubusercontent.com/35620465/44072727-92dfd6e8-9fcb-11e8-981c-fd80e91e0da3.jpg)


## 4주차 교육 : Jasmine을 활용한 TDD 로또 프로그램 구현

    ex)describe("getRandomNum 함수는",  function(){
	    it("1~45 사이의 수 반환한다.",  function(){
		    for(let  i  =  0;  i<1000;  i++){    
			    let  one_rand_num  =  getRandomNum()
			    expect(parseInt(one_rand_num)).toBe(one_rand_num)
			    expect(one_rand_num).toBeGreaterThanOrEqual(1)
			    expect(one_rand_num).toBeLessThanOrEqual(45)    
		    }
	    })
    })
    ex)describe("checkDuplicatedNum 함수는",  function(){    
	    it("([1, 7, 5, 3, 6, 10], 1)에 대해서 중복이 있다.",  function(){
		    expect(checkDuplicatedNum([1,  7,  5,  3,  6,  10],  1)).toBeTruthy()
	    })
	    it("([11, 27, 16, 23, 41, 19], 9)에 대해서 중복이 없다.",  function(){    
		    expect(checkDuplicatedNum([11,  27,  16,  23,  41,  19],  9)).toBeFalsy()
	    })    
    })
    ex)describe("getLottoNums 함수는",  function(){
	    it("6개의 랜덤 숫자를 중복없이 가져온다.",  function(){
		    let  six_num_list  =  getLottoNums()
		    expect(six_num_list.length).toBe(6)
		    expect(checkDuplicatedNumInList(six_num_list)).toBeFalsy()
	    })
    })
