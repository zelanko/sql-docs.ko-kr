---
title: 변수 값 파일 (AccessToSQL) 만들기 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 00144c51e60b72fe043443d2a9c8d1d51a6cb8da
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52542057"
---
# <a name="creating-variable-value-files-accesstosql"></a>변수 값 파일 (AccessToSQL) 만들기
변수 값 파일을 XML 파일 (예: 소스 또는 대상 서버 이름)에 서버 마이그레이션 간에 자주 변경 되는 명령의 매개 변수 값을 비교 됩니다. 원본 서버의 각 값을 저장 하는 것에 대 한 여러 변수 파일을 만들고 사용 하 여 마스터 스크립트 파일에서 참조 된 많은 수의 데이터베이스 마이그레이션 발생 합니다 **-v** 명령줄에서 전환 합니다. 이 동작은 여러 변수 파일에서 변수 값을 사용 하 여 몇 가지 스크립트 파일에 정적 값을 유지 관리에 도움이 됩니다.  
  
> [!NOTE]  
> -  변수 이름은 접두사를 $ (달러) 기호가 붙습니다. 변수는 변수 값 파일에서 값을 할당 되지 않은 경우 스크립트 파일의 구문 분석 하는 동안 오류가 발생 합니다 상태일 콘솔 실행 프로세스의 결과.  
> -  이스케이프 문자 **$** 됩니다 **$$** 합니다. 포함 된 매개 변수 또는 정적 값의 값을 **$** (달러) 기호를 다음 **$$** 변수 대신 문자로 취급 되도록 지정 해야 합니다.  
> -  유지 관리를 위해 변수를 선언할 수 내부 `'variable-group'` 사용자 정의 변수의 논리적 분리에 대 한 요소입니다.  이 요소의 사용 필수 아닙니다.  
  
**예:**  
  
**예제 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$type$" value="MyProject"/>  
  
    <variable name="$project_folder$" value=".\$project_name$"/>  
  
    <variable name="$project_name$" value="$type$ConsoleProject"/>  
  
    <variable name="$project_overwrite$" value="true"/>  
  
    <variable name="$project_type$" value="sql-server-2008"/>  
  
  </variable-group>  
  
</variables>  
```  
**예제 2:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="xxx"/>  
  
      <variable name="$TargetDB$" value="xxx"/>  
  
      <variable name="$TargetUserName$" value="xxx"/>  
  
      <variable name="$TargetPassword$" value="xxx"/>  
  
      <variable name="$TargetIsTrusted$" value="xxx"/>  
  
      <variable name="$TrustedConnection$" value="xxx"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="TestTable1"/>  
  
      <variable name="$ObjectName2$" value="TestProc1"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="variable-value-file-validation"></a>변수 값 파일 유효성 검사  
사용자 스키마 정의 파일에 대해 자신의 변수 값 파일을 쉽게 확인할 수 있습니다 **ConsoleScriptVariablesSchema.xsd** 'Schemas' 폴더에서 사용할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
운영 콘솔에서 다음 단계 [서버 연결 파일 만들기 &#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>참고자료  
[서버 연결 파일 (액세스) 만들기](https://msdn.microsoft.com/829153be-aa8e-4162-87e8-69882feecf19)  
  
