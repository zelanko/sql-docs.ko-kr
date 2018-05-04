---
title: SSMA 콘솔 (DB2ToSQL)의 명령줄 옵션 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 237354e9-25c4-4386-9d1f-ca0618d4a9a0
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3fbe09dac1c740c38bf958b78f2bd01f56bd80ad
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="command-line-options-in-ssma-console-db2tosql"></a>SSMA 콘솔 (DB2ToSQL)의 명령줄 옵션
Microsoft은 SSMA 작업을 제어를 실행 하는 강력한 집합 명령줄 옵션을 제공 합니다. 마샬링과 이후 섹션에서 자세히 설명 동일 합니다.  
  
## <a name="command-line-options-in-ssma-console"></a>SSMA 콘솔에서 명령줄 옵션  
설명 하는 콘솔 명령 옵션입니다.  
  
이 섹션에서는 목적으로 'option' 용어는 라고도 'switch'.  
  
옵션 대/소문자 구분 하지 않으며 사용 하 여 시작할 수 있습니다 '**-**'또는,'**/**' 문자입니다.  
  
옵션을 지정 하는 경우를 해당 옵션 매개 변수 지정 됩니다.  
  
옵션 매개 변수는 공백을 옵션 문자에서 구분 되어야 합니다.  
  
**구문 예제:**  
  
`C:\> SSMAforDB2Console.EXE -s scriptfile`  
  
`C:\> SSMAforDB2Console.EXE -s “C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \AssessmentReportGenerationSample.xml” –v “C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \VariableValueFileSample.xml” –c “C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ServersConnectionFileSample.xml”`  
  
큰따옴표 공백이 포함 된 폴더 또는 파일 이름은 지정 해야 합니다.  
  
명령줄 항목 및 오류 메시지의 출력은 stdout에서 또는 지정된 된 파일에 저장 됩니다.  
  
### <a name="script-file-option-sscript"></a>스크립트 파일 옵션:-s/스크립트  
필수 스위치 스크립트 파일 경로/이름 SSMA에서 실행할 명령 시퀀스의 스크립트를 지정 합니다.  
  
**구문 예제:**  
  
`C:\>SSMAforDB2Console.EXE –s “C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”`  
  
### <a name="variable-value-file-option-vvariable"></a>변수 값 파일 옵션:-v/변수  
이 파일 스크립트 파일에 사용 되는 변수를 구성 합니다. 선택적 스위치입니다. 변수 되지 변수 파일에 선언 하 고 스크립트 파일에 사용 되는 응용 프로그램에서 오류를 생성 하 고 콘솔 실행을 종료 합니다.  
  
**구문 예제:**  
  
-   기본값은 아마도 하나 및 해당 하는 경우 인스턴스 특정 값을 가진 다른 여러 변수 값 파일에 정의 된 변수입니다. 명령줄 인수에 지정 된 마지막 변수 파일은 변수의 중복이 발생 된 경우에 된 기본 설정을 사용 합니다.  
  
    `C:\>SSMAforDB2Console.EXE -s`  
  
    `“C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml” –v c:\migration`  
  
    `projects\global_variablevaluefile.xml –v “c:\migrationprojects\instance_variablevaluefile.xml”`  
  
### <a name="server-connection-file-option-cserverconnection"></a>서버 연결 파일 옵션:-c/serverconnection  
이 파일에는 각 서버에 대 한 서버 연결 정보가 포함 됩니다. 각 서버 정의 id입니다. 고유한 서버도 식별 서버 Id 연결에 대 한 스크립트 파일에서 참조 되는 관련 된 명령을 합니다.  
  
서버 정의 서버 연결 파일 및/또는 스크립트 파일의 일부를 수 있습니다. 스크립트 파일에서 서버 id 서버 id의 중복이 발생 된 경우에 서버 연결 파일 보다 우선 합니다.  
  
**구문 예제:**  
  
-   서버 Id는 스크립트 파일에 사용 되 나, 별도 서버 연결 파일에 정의 된 변수 값 파일에 정의 된 변수를 사용 하는 서버 연결 파일:  
  
    `C:\>SSMAforDB2Console.EXE –s “C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –v`  
  
    `c:\SsmaProjects\myvaluefile1.xml –c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   서버 정의 스크립트 파일에 포함 됩니다.  
  
    `C:\>SSMAforDB2Console.EXE –s “C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>XML 출력 옵션:-x / xmloutput [xmloutputfile]  
이 명령은 콘솔 이나 xml 파일에 xml 형식에서 명령 출력 메시지를 출력 하는 중에 사용 됩니다.  
  
두 가지 옵션이 있습니다 xmloutput에 사용할 수 있는 viz 하십시오..,:  
  
-   Filepath xmloutput 전환 된 후 제공 된 경우 출력 파일에 리디렉션됩니다.  
  
    **구문 예제:**  
  
    `C:\>SSMAforDB2Console.EXE –s`  
  
    `“C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –x d:\xmloutput\project1output.xml`  
  
-   없는 filepath xmloutput 스위치 다음 제공 된 경우는 xmlout 자체 콘솔에 표시 됩니다.  
  
    **구문 예제:**  
  
    `C:\>SSMAforDB2Console.EXE –s “C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –xmloutput`  
  
### <a name="log-file-option-llog"></a>로그 파일 옵션: – l/로그  
콘솔 응용 프로그램의 모든 SSMA 작업이 로그 파일에 기록 합니다. 선택적 스위치입니다. 로그 파일 및 설치 경로 명령줄에서 지정 경우 지정된 된 위치에 로그 생성을 가져옵니다. 그렇지 않으면 기본 위치에 생성 되기 합니다.  
  
**구문 예제:**  
  
`C:\>SSMAforDB2Console.EXE`  
  
`“C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option-eprojectenvironment"></a>– E/projectenvironment 프로젝트 환경 폴더 옵션:  
현재 SSMA 프로젝트에 대 한 프로젝트 환경 설정 폴더를 나타냅니다. 이 스위치는 선택 사항입니다.  
  
**구문 예제:**  
  
`C:\>SSMAforDB2Console.EXE –s`  
  
`“C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –e c:\SsmaProjects\CommonEnvironment`  
  
### <a name="secure-password-option-psecurepassword"></a>– P/securepassword 보안 암호 옵션:  
이 옵션은 서버 연결에 대 한 암호화 된 암호를 나타냅니다. 다른 모든 옵션에서 다른: 옵션 모든 스크립트를 실행 아니고 모든 마이그레이션 관련 작업에 유용 하지만 마이그레이션 프로젝트에서 사용 되는 서버 연결에 대 한 암호 암호화를 관리 하는 데 도움이 됩니다.  
  
명령줄 매개 변수로 옵션이 나 암호를 입력할 수 없습니다. 그렇지 않으면 오류가 발생합니다. 자세한 내용은 참조는 [암호 관리](http://msdn.microsoft.com/en-us/56d546e3-8747-4169-aace-693302667e94) 섹션.  
  
다음 하위 옵션에 대해 지원 됩니다 `–p/securepassword`:  
  
-   암호를 추가 하려면 서버 연결 파일에 정의 된 모든 서버 Id 또는 지정 된 서버 ID에 대 한 저장소를 보호 합니다. -Overwrite 옵션을 업데이트 아래 암호 이미 있는 경우:  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}` `-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-s|-script <server-connection-file> [-v|variable <variable-value-file>] [-o|overwrite]`  
  
-   에 지정된 된 서버 ID의 또는 모든 서버 Id에 대 한 보호 된 저장소에서 암호화 된 암호를 제거 합니다.  
  
    `–p/securepassword –r/remove {<server_id> [, …n] | all}`  
  
-   암호를 암호화 하는 서버 Id의 목록을 표시 합니다.  
  
    `–p/securepassword –l/list`  
  
-   암호화 된 파일에 보호 된 저장소에 저장 된 암호를 내보내려면 합니다. 이 파일은 사용자가 지정한 암호와 암호화 됩니다.  
  
    `–p/securepassword –e/export {<server-id> [, …n] | all} <encrypted-password -file>`  
  
-   사용자가 지정한 암호를 사용 하 여 로컬 보호 된 저장소는 암호화-내보낸 파일은 이전 가져오게 됩니다. 파일 해독 하는 경우에 로컬 컴퓨터에서 암호화는 새 파일에 저장 됩니다.  
  
    `–p/securepassword –i/import {<server-id> [, …n] | all} <encrypted-password -file>`  
  
    쉼표 구분 기호를 사용 하 여 여러 서버 Id는 지정할 수 있습니다.  
  
### <a name="help-option-help"></a>도움말 옵션:-? / h  
SSMA 콘솔 옵션의 구문 요약 정보를 표시합니다.  
  
`C:\>SSMAforDB2Console.EXE -?`  
  
SSMA 콘솔 명령줄 옵션의 테이블 형식으로 출력, 참조 [부록-1 &#40;DB2ToSQL&#41;](../../ssma/db2/appendix-1-db2tosql.md)합니다.  
  
### <a name="securepassword-help-option-securepassword--help"></a>Securepassword – SecurePassword 도움말 옵션:-? / h  
SSMA 콘솔 옵션의 구문 요약 정보를 표시합니다.  
  
`C:\>SSMAforDB2Console.EXE -securepassword -?`  
  
SSMA 콘솔 명령줄 옵션의 테이블 형식으로 출력, 참조 [부록-1 &#40;DB2ToSQL&#41;](../../ssma/db2/appendix-1-db2tosql.md)  
  
### <a name="next-step"></a>다음 단계  
다음 단계에서는 프로젝트 요구 사항에 따라 달라 집니다.  
  
1.  암호 또는 내보내기 지정 하기 위한 암호 가져오기 /를 참조 하십시오 [암호 관리 &#40;DB2ToSQL&#41;](../../ssma/db2/managing-passwords-db2tosql.md)합니다.  
  
2.  보고서를 생성 하는 것에 대 한 참조 [보고서 생성 &#40;DB2ToSQL&#41;](../../ssma/db2/generating-reports-db2tosql.md)합니다.  
  
3.  콘솔에서 문제를 해결 하는 것에 대 한 참조 [문제 해결 &#40;DB2ToSQL&#41;](../../ssma/db2/troubleshooting-db2tosql.md)합니다.  
  
