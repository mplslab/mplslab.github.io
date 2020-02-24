```XML

//·Case·1)·Select·Syntax·-·standard
<!--
····사용자·정보를·조회한다.
····2020.02.17····jsjeon····주소·추가·관련·NATION_FLAG·추가
-->
<select·id="selectUser"·resultMap="userMap">
····/*·User.selectUser·*/
····SELECT··U.USERID
··········,·U.AUTH_CODE
··········,·(··········
··············CASE·WHEN·DC_CODE·IN·('CD45',·'CD50')·THEN·'CDHY'
···················WHEN·DC_CODE·IN·('CD35',·'CD40')·THEN·'CDZH'
···············END
············)·AS·REAL_DC_CODE
····FROM····USER······U·····--·회원
········,···USER_AUTH·UA····--·회원·권한
························································································
····WHERE···U.AUTH_CODE···=·UA.AUTH_CODE
····AND·····U.USERID······=·#{value}
····AND·····U.DELETE_FLAG·=·'N'
</select>

//·Case·2)·Select·Syntax·-·SubQuery
<select·id="selectUserList"·resultType="hashmap">
····/*·User.selectUserList·*/
····SELECT··T2.*
····FROM····(
··············SELECT··ROWNUM·RNUM,·T1.*
··············FROM····(
························SELECT··U.USERID
······························,·U.AUTH_CODE
······························,·TO_CHAR(U.FRST_OPER_DATE,·'YYYY.MM.DD')·AS·FRST_OPER_DATE
························FROM····USER·U
························WHERE···USER_ID·=·#{userId}

························<choose>
····························<when·test="searchAuthCode·==·'-1'.toString()">
································AND····U.AUTH_CODE·IS·NULL
····························</when>
····························<when·test="searchAuthCode·!=·'-1'.toString()">
································AND····U.AUTH_CODE·=·#{searchAuthCode}
····························</when>
························</choose>

························ORDER·BY·FRST_OPER_DATE·DESC
······················)·T1
··············WHERE···ROWNUM·=·#{lastRecordIndex}
············)·T2
····WHERE···RNUM·=·#{firstRecordIndex}
</select>

//·Case·2)·Select·Syntax·-·Inline·View
<select·id="selectEmpList"·resultType="hashmap">
····/*·User.selectEmpList·*/
····SELECT··B.EMPNO
··········,·B.ENAME
····FROM····(
··············SELECT··EMPNO
··············FROM····EMP
··············WHERE···SAL·=·(
······························SELECT··AVG(SAL)
······························FROM····EMP
······························WHERE···DEPTNO·=·20
····························)
············)···A
··········,·EMP·B
····WHERE···A.EMPNO·=·B.EMPNO
····AND·····B.MGR·IS·NOT·NULL
····AND·····B.DEPTNO·!=·20
</select>

















··```