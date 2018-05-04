---
title: SSMA는 Sybase 콘솔 (SybaseToSQL)에 대 한 시작 | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Launching SSMA Console
- Sybase Console,Output Conventions
- Sybase Console,Procedure for Using Console
ms.assetid: 43219dbe-bcfa-427d-9242-f07b1455f15f
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0b7e1ced397dfd651161a2c7fb50622f413ad0e9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getting-started-with-the-ssma-for-sybase-console-sybasetosql"></a>SSMA는 Sybase 콘솔 (SybaseToSQL)에 대 한 시작
이 섹션에서는를 시작 하 고 SSMA Sybase 콘솔 응용 프로그램에 대 한 시작 프로시저가 설명 합니다. 또한 여기에 나열 된 규칙에에서 사용 됩니다 일반적인 SSMA 콘솔 출력 창.  
  
## <a name="launching-the-ssma-console"></a>SSMA 콘솔 시작  
SSMA 콘솔 응용 프로그램을 시작 하려면 다음 단계를 사용 합니다.  
  
1.  시작을 이동한 다음 모든 프로그램을 가리킵니다.  
  
2.  클릭는 **SQL Server Migration Assistant Sybase 명령 프롬프트에 대 한** 바로 가기 합니다.  
  
    SSMA 콘솔 사용 메뉴를 표시 하 고 `(/? Help)`, 콘솔 응용 프로그램을 시작할 수 있도록 합니다.  
  
## <a name="using-the-ssma-console"></a>SSMA 콘솔을 사용 하 여  
Windows 시스템에 콘솔이 성공적으로 시작 후에 작업을 다음 단계를 사용할 수 있습니다.  
  
1.  SSMA 콘솔 스크립트 파일을 통해 구성 합니다. 이 섹션에 대 한 자세한 내용은 참조 하십시오. [스크립트 파일 만들기 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md)합니다.  
  
2.  [변수 값 파일을 만드는 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [서버 연결 파일 만들기 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [SSMA 콘솔 실행 &#40;SybaseToSQL&#41; ](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) 프로젝트 요구 사항에 기반 합니다. 
  
추가 기능:  
  
1.  [암호를 지정](http://msdn.microsoft.com/en-us/9b6a70f9-6840-4140-a059-bb7bd7ccc67c) 및 내보내기/가져오기 것 다른 창 컴퓨터에 있습니다.  
  
2.  [보고서를 생성할](http://msdn.microsoft.com/en-us/19278f6a-6d58-4867-9d71-c6228040466e) 자세한 xml을 보려면 평가/변환 및 데이터 마이그레이션에 대 한 보고서를 출력 합니다. 새로 고침 및 동기화 명령에 대 한 자세한 오류 보고서를 생성할 수 있습니다.  
  
## <a name="ssma-console-output-conventions"></a>SSMA 콘솔 출력 규칙  
SSMA 스크립트 명령 및 옵션을 실행 시 콘솔 프로그램 결과 및 메시지 (정보, 오류 등)를 콘솔에 표시 하는 또는 필요에 따라 xml 출력 파일로 리디렉션합니다. 각 유형의 메시지 출력에는 고유한 색으로 표시 됩니다. 예를 들어 흰색에 문자 메시지가 나타냅니다 스크립트 파일 명령을입니다. 녹색의 사용자 입력에 대 한 프롬프트 및 등을 나타냅니다.  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
콘솔 출력의 색 해석 다음 표에 표시 됩니다.  
  
|색|Description|  
|---------|---------------|  
|빨강|실행 하는 동안 심각한 오류|  
|회색|날짜 및 시간 스탬프를 사용자에 게 메시지|  
|흰색|스크립트 파일 명령, 메시지 유형|  
|노란색|경고|  
|녹색|사용자 입력에 대 한 프롬프트|  
|녹청|시작, 완료 및 작업의 결과|  
  
## <a name="see-also"></a>참고 항목  
[SAP ASE 용 SSMA를 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
