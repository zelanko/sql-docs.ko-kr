---
title: "변수 값 파일 (SybaseToSQL) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Creating Variable Value Files
- Sybase Console,Variable Value File Validation
ms.assetid: 395be464-4b19-44f7-91e5-b8876d6743dc
caps.latest.revision: "15"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 28fadfc4f54f68a6459cc3f3cef4df91967e5e52
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="creating-variable-value-files-sybasetosql"></a>변수 값 파일 (SybaseToSQL) 만들기
변수 값 파일은 다른 하나의 서버 마이그레이션의 자주 변경 하는 원본 또는 대상 서버 이름이 같은 명령의 매개 변수 값을 구성 하는 XML 파일입니다. 데이터베이스 마이그레이션 다 수 발생 하는 경우 원본 서버의 각 값을 저장 하기 위한 여러 변수 파일을 만든 포함 마스터 스크립트 파일에서 참조 되는 **– v** 명령줄에서 전환 합니다. 이렇게 하면 여러 변수 파일에서 변수 값이 포함 된 몇 가지 스크립트 파일에 정적 값을 유지 관리 합니다.  
  
> [!NOTE]  
> 1.  변수 이름은 접두사를 $ (달러) 기호 접미사. 변수는 변수 값 파일의 값이 지정 되지 않은 경우에 콘솔 실행 프로세스 시간으로 인해 발생 하는 스크립트 파일의 구문 분석 하는 동안 오류가 발생 합니다.  
> 2.  The escape character for **$** is **$$**. 매개 변수 또는 정적 값의 값에 포함 된 경우  **$**  (달러) 기호를 다음  **$$**  변수 대신 문자로 취급 되도록 지정 해야 합니다.  
> 3.  유지 관리 용이성을 위해 변수를 선언할 수 내부 `‘variable-group’` 사용자의 논리적 분리에 대 한 요소는 변수를 정의 합니다.  사용 현황이 요소는 필수입니다.  
  
**예:**  
  
**예제 1:**  
  
```xml  
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
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetUserName$" value="<user-name>"/>  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
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
  
## <a name="variable-value-file-validation"></a>변수 값 파일 유효성 검사  
사용자는 스키마 정의 파일에 대해 자신의 변수 값 파일 유효성을 검사할 쉽게 수 **ConsoleScriptVariablesSchema.xsd** '스키마' 폴더에서 사용할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
운영 콘솔에 다음 단계는 [서버 연결 파일 &#40; 만들기 SybaseToSQL &#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
## <a name="see-also"></a>관련 항목:  
[서버 파일 (Sybase) 만들기](http://msdn.microsoft.com/en-us/35ef396f-9f98-429d-9fc5-4f413d08fb37)  
  
