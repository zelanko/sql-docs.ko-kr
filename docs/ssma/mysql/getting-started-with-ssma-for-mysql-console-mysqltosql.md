---
title: MySQL 콘솔 (MySQLToSQL) 용 SSMA 시작 | Microsoft Docs
ms.prod: sql
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
helpviewer_keywords:
- MySQL Console, launching console
- MySQL Console, output conventions
ms.assetid: 218d502c-059f-4d48-9aea-61e553d74303
caps.latest.revision: 23
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 75e189d89c9a1bbc7207521b8156d0f4b56ca759
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34776239"
---
# <a name="getting-started-with-ssma-for-mysql-console-mysqltosql"></a>MySQL 콘솔 (MySQLToSQL) 용 SSMA 시작
이 섹션에서는 시작 하 고 MySQL 콘솔 응용 프로그램을 시작 하는 절차를 설명 합니다. 또한 나열 된 여기에 규칙이 사용 일반적인 SSMA 콘솔 출력 창에.  
  
## <a name="launching-ssma-console"></a>SSMA 콘솔 시작  
SSMA 콘솔 응용 프로그램을 시작 하려면 다음 단계를 사용 합니다.  
  
1.  로 이동 **시작** 를 가리키도록 **모든 프로그램**합니다.  
  
2.  클릭는 **SQL Server Migration Assistant MySQL 명령 프롬프트에 대 한** 바로 가기 합니다.  
  
    SSMA 콘솔 사용 메뉴를 표시 하 고 `(/? Help)`, 콘솔 응용 프로그램을 시작할 수 있도록 합니다.  
  
## <a name="procedure-for-using-the-ssma-console"></a>SSMA 콘솔을 사용 하기 위한 절차  
Windows 시스템에 콘솔이 성공적으로 시작 후에 작업을 다음 단계를 사용할 수 있습니다.  
  
1.  SSMA 콘솔 스크립트 파일을 통해 구성 합니다. 이 섹션에 대 한 자세한 내용은 참조 하십시오. [스크립트 파일 만들기 &#40;MySQLToSQL&#41; ](../../ssma/mysql/creating-script-files-mysqltosql.md) 합니다.  
  
2.  [변수 값 파일을 만드는 &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
  
3.  [서버 연결 파일 만들기 &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
4.  [SSMA 콘솔 실행 &#40;MySQLToSQL&#41; ](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md) 프로젝트 요구 사항에 따라  
  
추가 기능:  
  
1.  [암호 보안](http://msdn.microsoft.com/en-us/4ffbc587-ea3f-49ad-bc42-a654f672325e) 다른 창 컴퓨터 가져오기 / 내보내기 하 고  
  
2.  [보고서를 생성할](http://msdn.microsoft.com/en-us/1c0202e8-546d-4cb3-a37f-1d2e35d53839) 자세한 xml을 보려면 평가 /conversion 및 데이터 마이그레이션에 대 한 보고서를 출력 합니다. 새로 고침 및 동기화 명령에 대 한 자세한 오류 보고서를 생성할 수도 있습니다.  
  
## <a name="ssma-console-output-conventions"></a>SSMA 콘솔 출력 규칙  
SSMA 스크립트 명령 및 옵션을 실행 결과 및 메시지 (정보, 오류 등)를 콘솔에 표시 하는 콘솔 프로그램 만들거나 필요한 경우 xml 출력 파일로 리디렉션합니다. 각 유형의 메시지 출력에는 고유한 색으로 표시 됩니다. 예를 들어 흰색에 문자 메시지가 나타냅니다 스크립트 파일 명령을입니다. 녹색의 사용자 입력에 대 한 프롬프트 및 등을 나타냅니다.  
  
![SSMAConsoleOutput_MySQL](../../ssma/mysql/media/ssmaconsoleoutput_mysql.jpg "SSMAConsoleOutput_MySQL")  
  
다음 표에서 콘솔 출력의 색을 해석:  
  
|색|Description|  
|---------|---------------|  
|빨강|실행 하는 동안 심각한 오류|  
|회색|날짜 및 시간 스탬프를 사용자에 게 메시지|  
|흰색|스크립트 파일 명령, 메시지 유형|  
|노란색|경고|  
|녹색|사용자 입력에 대 한 프롬프트|  
|녹청|시작, 완료 및 작업의 결과|  
  
## <a name="see-also"></a>관련 항목  
[MySQL 용 SSMA를 설치합니다.](http://msdn.microsoft.com/en-us/e89b45bd-59c1-4d23-8bd7-3dafc1947448)  
  
