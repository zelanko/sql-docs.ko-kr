---
title: 변수 값 파일 (DB2ToSQL) 만들기 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 122f3fbe-46a0-40df-ac3b-d43bf33d96ba
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: cf62d09de1180687598d817ff9199d7098008829
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63299139"
---
# <a name="creating-variable-value-files-db2tosql"></a>변수 값 파일 (DB2ToSQL) 만들기
변수 값 파일은 다른 서버 마이그레이션에서 자주 변경 하는 원본 또는 대상 서버 이름과 같은 명령의 매개 변수 값을 비교 하는 XML 파일입니다. 많은 수의 데이터베이스 마이그레이션 수행 하는 경우 원본 서버의 각 값을 저장 하는 것에 대 한 여러 변수 파일을 만든 마스터 스크립트 파일의 참조를 **-v** 명령줄에서 전환 합니다. 이 여러 변수 파일에서 변수 값을 사용 하 여 몇 가지 스크립트 파일에 정적 값을 유지 관리에 도움이 됩니다.  
  
> [!NOTE]  
> 1.  변수 이름은 접두사를 $ (달러) 기호가 붙습니다. 변수를 변수 값 파일에서 값이 지정 되지 않은 경우 상태일 콘솔 실행 프로세스의 결과 스크립트 파일의 구문 분석 하는 동안 오류가 발생 합니다.  
> 2.  이스케이프 문자 **$** 됩니다 **$$** 합니다. 매개 변수 또는 정적 값의 값이 있으면 **$** (달러) 기호, 한 다음 **$$** 변수 대신 문자로 취급 되도록 지정 해야 합니다.  
> 3.  유지 관리를 위해 변수를 선언할 수 내부 `'variable-group'` 사용자의 논리적 분리에 대 한 요소 변수를 정의 합니다.  이 요소의 사용 필수 아닙니다.  
  
**예:**  
  
**예제 1:**  
  
```  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$project_folder$" value="<project-folder>"/>  
  
    <variable name="$project_name$" value="<project-name>"/>  
  
    <variable name="$project_overwrite$" value="<true/false>"/>  
  
    <variable name="$project_type$" value="<project-type>"/>  
  
  </variable-group>  
  
</variables>  
```  
**예제 2:**  
  
```  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
      <variable name="$TargetUserName$" value="<user-name>"/>  
  
      <variable name="$TargetPassword$" value="<password>"/>  
  
      <variable name="$TrustedConnection$" value="<true/false>"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="<object-name>"/>  
  
      <variable name="$ObjectName2$" value="<object-name>"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="next-step"></a>다음 단계  
운영 콘솔에서 다음 단계 [서버 연결 파일 만들기 &#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
## <a name="see-also"></a>관련 항목  
[서버 연결 파일 만들기](../oracle/creating-the-server-connection-files-oracletosql.md)  
  
