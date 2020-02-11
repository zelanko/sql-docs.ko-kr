---
title: 변수 값 파일 만들기 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 051ded7d675f81998718b858c71488ba968ec680
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006599"
---
# <a name="creating-variable-value-files-accesstosql"></a>변수 값 파일 만들기 (AccessToSQL)
변수 값 파일은 서버 마이그레이션 간에 자주 변경 되는 명령 (예: 원본 또는 대상 서버 이름)의 매개 변수 값을 구성 하는 XML 파일입니다. 데이터베이스 마이그레이션이 많이 발생 하면 각 원본 서버의 값을 저장 하기 위한 여러 변수 파일이 생성 되 고 명령줄에서 **-v** 스위치를 사용 하 여 마스터 스크립트 파일에 참조 됩니다. 이 동작은 여러 변수 파일의 변수 값을 사용 하 여 몇 가지 스크립트 파일의 정적 값을 유지 하는 데 도움이 됩니다.  
  
> [!NOTE]  
> -  변수 이름 앞에는 $ (달러) 기호가 붙습니다. 변수에 변수 값 파일의 값이 할당 되지 않은 경우 스크립트 파일의 구문 분석 중에 오류가 발생 하 여 콘솔 실행 프로세스가 상태일 됩니다.  
> -  에 대 한 **$** 이스케이프 문자 **$$** 는입니다. 매개 변수의 변수 또는 정적 값이 (달러) 기호를 **$** 포함 하는 경우를 변수 대신 문자로 **$$** 처리 하도록 지정 해야 합니다.  
> -  유지 관리를 위해 변수를 요소 내 `'variable-group'` 에 선언 하 여 사용자 정의 변수를 논리적으로 분리할 수 있습니다.  이 요소는 반드시 사용 해야 하는 것은 아닙니다.  
  
**예:**  
  
**예 1:**  
  
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
**예 2:**  
  
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
사용자는 ' 스키마 ' 폴더에서 사용할 수 있는 **ConsoleScriptVariablesSchema** 스키마 정의 파일에 대해 해당 변수 값 파일의 유효성을 쉽게 검사할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
콘솔 운영의 다음 단계에서는 [AccessToSQL &#40;서버 연결 파일을 만듭니다&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>참고 항목  
[서버 연결 파일 만들기 (Access)](https://msdn.microsoft.com/829153be-aa8e-4162-87e8-69882feecf19)  
  
