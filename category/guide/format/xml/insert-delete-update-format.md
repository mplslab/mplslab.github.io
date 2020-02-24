```xml

//·Insert·Syntax·-·standard
<!--
····회원·정보를·등록한다.
····2020.02.17····jsjeon····init
-->
<insert·id="insertUser">
····/*·User.insertUser·*/
····INSERT·INTO·USER·(
··········USERID
········,·AUTH_CODE
········,·PWD
········,·NAME
····)
····VALUES·(
··········#{userid}
········,·#{authCode}
········,·#{pwd}
········,·#{name}
····)
</insert>

//·Update·Syntax·-·standard
<!--
····회원·정보를·수정한다.
····2020.02.17····jsjeon····init
-->
<update·id="updateUser">
····/*·User.updateUser·*/
····UPDATE··USER
····SET·····NAME···········=·#{name}
··········,·PIN············=·#{pin}
··········,·GENDER·········=·#{gender}
···························································
············<if·test="authCode·!=·null·and·authCode·!=·''">
················,·AUTH_CODE·=·#{authCode}
············</if>
···························································
············<if·test="pwd·!=·null·and·pwd·!=·''">
················,·PWD·=·#{pwd}
············</if>
···························································
····WHERE···USERID·=·#{userid}
</update>

//·Delete·Syntax·-·standard
<!--
····회원·정보를·삭제한다.
····2020.02.17····jsjeon····init
-->
<delete·id="deleteUser">
····/*·User.deleteUser·*/
····DELETE
····FROM····USER
····WHERE···USER_ID·=·#{userId}
····AND·····DEL_YN··=·'N'
</delete>




```
