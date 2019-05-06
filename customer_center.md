- customer_center.js

```js
$('.submit_btn').click(function() {
  let inputName = $('.input_name').val();
  let inputPhone = $('.input_phone').val();
  let inputEmail = $('.input_email').val();
  let inputContent = $('.input_content').val();
  let regExp = /^[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*.[a-zA-Z]{2,3}$/i;
  let termsAgree = $('input:checkbox[id="terms_agree"]').is(':checked');
  let marketingAgree = $('input:checkbox[id="marketing_agree"]').is(':checked');
  let errFlag = true;
  
  // 이름
  if (inputName === '') {
    $('.name_error').html('필수 입력 항목입니다.');
    $('.input_name').css('border', '2px solid #fe0000');
    errFlag = false;
  } else {
    $('.name_error').html('');
    $('.input_name').css('border', '1px solid #ced4da');
  }
  
  // 연락처
  if (inputPhone === '') {
    $('.phone_error').html('필수 입력 항목입니다.');
    $('.input_phone').css('border', '2px solid #fe0000');
    errFlag = false;
  } else {
    $('.phone_error').html('');
    $('.input_phone').css('border', '1px solid #ced4da');
  }
  
  // 이메일
  if (inputEmail.match(regExp) === null) {
    $('.email_error').html('올바른 이메일 형식으로 입력해주세요.');
    $('.input_email').css('border', '2px solid #fe0000');
    errFlag = false;
  } else {
    $('.email_error').html('');
    $('.input_email').css('border', '1px solid #ced4da');
  }
  
  // 내용
  if (inputContent === '') {
    $('.content_error').html('필수 입력 항목입니다.');
    $('.input_content').css('border', '2px solid #fe0000');
    errFlag = false;
  } else {
    $('.content_error').html('');
    $('.input_content').css('border', '1px solid #ced4da');
  }
  
  if (errFlag === false) {
    return;
  }
  
  if (termsAgree === false) {
    alert('이용약관에 동의해야 합니다.');
    errFlag = false;
  }
  
  let result = {
    inputName: inputName,
    inputPhone: inputPhone,
    inputEmail: inputEmail,
    inputContent: inputContent,
    termsAgree: termsAgree,
    marketingAgree: marketingAgree
  };
  
  if (errFlag === true) {
    console.log('SUCCESS');
    console.log(result);
    alert('정상적으로 제출되었습니다.');
  } else {
    return;
  }
});
```

<br>