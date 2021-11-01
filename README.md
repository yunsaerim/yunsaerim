* 경제학과 (20170842) 윤새림 모바일 프로그래밍 개인과제



## 1. 화면별 구현된 기능

### 첫번째 화면 (Relative Layout 혹은 Fragment 사용)
- [ ] 앱 접속 페이지, 회원 ID/비밀번호(EditView), 로그인/회원가입(Button)
- [x] 첫번째 화면 초기화시에 기존에 저장된 개인정보 읽어 오기
- [x] ID, 비밀번호 입력 시 기존에 가입한 회원 ID, 비밀번호 체크 오류 시 에러 메시지 출력
- [x] ID, 비밀번호 입력이 정상이고 로그인 버튼 클릭 시 세번째 페이지 이동
- [ ] 회원가입 없이도 메인 버튼(상품 출력 페이지)을 클릭하면 세번째 화면으로 이동 가능 

### 두번째 화면 (Linear Layout 혹은 Fragment 사용)
- [ ] 회원가입 페이지, 첫번째 페이지에서 회원가입 버튼 클릭 시 출력
- [x] ID(EditView, 중복검사)
- [ ] 비밀번호(EditView, 자릿수/특수키 등 규칙 체크)
- [ ] 이름/전화번호/주소(EditView)
- [ ] 개인정보 사용 동의 간략 약관(TextView), 동의 여부(Radio Button, Decline/Accept)
- [ ] 회원정보를 저장하고 첫번째 페이지로 이동   
  *회원정보 저장은 전역변수, 프레퍼런스(Preference), 파일 활용

### 세번째 화면 (Constraint Layout, Table Layout, Grid Layout, Frame Layout 중 하나 사용)
- [ ] 상품명, 상품이미지 리스트를 보여주는 화면 (5개이상 이미지를 기본으로 출력)
- [x] 화면 아래 부분에서 상품명, 상품이미지를 등록 및 삭제하는 버튼 추가
- [x] 화면 아래 부분에 회원정보 버튼은 회원인 경우는 가입한 회원 정보를 보여주고
  회원이 아닌 경우는 회원정보 버튼을 클릭하면 회원가입 여부를 물어보고
  원하면 회원가입 페이지인 두번째 화면으로 이동 
- [x] View을 상속한 여러가지 위젯을 사용하여 화면을 구성(기능에 맞는 위젯 선택하여 구성)
  View Group을 상속한 위젯 ListView, GridView, AdapterView, ToolBar 등
  Text View을 상속한 CheckBox, Switch, ToggleButton, RadioButton 등
  ImageView, ImageButton 등

<br/>   

## 2. 상세 구현 내용
로그인화면(첫번째 Activity) UI구성은 했으나, SharedPreference로 값을 저장하고, 저장한 값으로 id와 pw를 매칭하여 로그인이 되도록 하는 것을 구현하지 못했습니다. 빈칸일 경우 toast가 뜨는 것은 구현했으나, 로그인을 하려하면 에러가 납니다. (SharedPreference를 처음접해보는 것이라 미숙) ImageButton을 클릭할 시 상품화면(세번째 Activity)으로 이동, 회원가입 버튼을 클릭할 시 회원가입화면(두번째 Activity)로 이동 하는 것을 intent로 구현했습니다. 

회원가입화면 (두번째 Activity) UI구성은 했으나, 이것 또한 SharedPreference를 잘 활용하지 못하여 중복검사를 구현하지 못했습니다. id, 비밀번호, 이름, 전화번호, 주소는 모두 EditView를 사용하여 값을 받을 수 있도록 했습니다. 비밀번호는 자릿수, 특수키 규칙을 적용하여 이를 충족하지 못할 시 toast메시지가 뜨게 구현했습니다. 개인정보 사용 동의 약관은 radio view와 radio button을 사용하여 "동의하지않습니다" 버튼 클릭시 toast메시지가 뜨게 구현했습니다. 모든 editView가 빈칸이 아니고, 비밀번호 규칙이 충족하고 동의약관 동의 시 '가입하기'버튼을 누르면 로그인 화면(첫번째 Activity)로 이동합니다. 

상품화면(세번째 Activity)는 listView를 adapt하여 구현하였습니다. 화면상으로 5개 리스트, 추가버튼, 회원정보 버튼은 구현했으나, 상품별 '삭제'버튼 구현과정에서 어려움을 겪어 구현하지 못했습니다. 상품추가 버튼 클릭, 회원정보 버튼 클릭시 오류가 발생합니다. 


## 3. 구현하지 못한 부분

        login_button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                id = idText.getText().toString();
                password = passwordText.getText().toString();


                if (id.equals("") || password.equals("")) {
                    Toast.makeText(getApplicationContext(), "빈칸이 존재합니다. 다시 입력해주세요.", Toast.LENGTH_SHORT).show();
                } else {
                        String userId = userPref.getString("id","");
                        String userPwd = userPref.getString("password","");
                    if (id.equals(userId) && password.equals(userPwd)) {
                        userInfo.userLogin(userId, userPwd);
                        Intent intent2 = new Intent(first_activity.this, third_activity.class);
                        intent2.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
                        intent2.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
                        startActivity(intent2);
                        finish();
                    } else {
                        Toast.makeText(getApplicationContext(), "아이디 혹은 비밀번호가 일치하지 않습니다.", Toast.LENGTH_SHORT).show();
                    }
                }
            }
        });

sharedPreference에 저장된 값을 활용하는 방법을 잘 모르겠습니다. 

