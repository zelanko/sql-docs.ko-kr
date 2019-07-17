---
title: Sybase 콘솔 (SybaseToSQL) 용 SSMA 시작 | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Launching SSMA Console
- Sybase Console,Output Conventions
- Sybase Console,Procedure for Using Console
ms.assetid: 43219dbe-bcfa-427d-9242-f07b1455f15f
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: bad08c06028a64a0423135b15641ebf6fa4e895e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029113"
---
# <a name="getting-started-with-the-ssma-for-sybase-console-sybasetosql"></a>Sybase 콘솔 (SybaseToSQL) 용 SSMA 시작
이 섹션에서는 시작 하 고 콘솔 응용 프로그램 Sybase 용 SSMA 시작 절차를 설명 합니다. 또한 여기에 나열 된 규칙에에서 사용 됩니다 일반적인 SSMA 콘솔 출력 창.  
  
## <a name="launching-the-ssma-console"></a>SSMA 콘솔 시작  
SSMA 콘솔 응용 프로그램을 시작 하려면 다음 단계를 사용 합니다.  
  
1.  시작을 이동한 다음 모든 프로그램을 가리킵니다.  
  
2.  클릭 합니다 **SQL Server Migration Assistant Sybase 명령 프롬프트에 대 한** 바로 가기.  
  
    SSMA 콘솔 사용 메뉴 표시 및 `(/? Help)`콘솔 응용 프로그램을 시작할 수 있도록 합니다.  
  
## <a name="using-the-ssma-console"></a>SSMA 콘솔을 사용 하 여  
콘솔 Windows 시스템에 성공적으로 시작 되 면 다음 단계에 작업을 사용할 수 있습니다.  
  
1.  SSMA 콘솔 스크립트 파일을 통해 구성 합니다. 이 섹션에 대 한 자세한 내용은 참조 하세요. [스크립트 파일 만들기 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md)합니다.  
  
2.  [변수 값 파일 만들기 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [서버 연결 파일 만들기 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [SSMA 콘솔 실행 &#40;SybaseToSQL&#41; ](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) 프로젝트 요구 사항에 따라 합니다. 
  
추가 기능:  
  
1.  [암호를 지정](managing-passwords-sybasetosql.md) 및 내보내기/가져오기 하에 다른 창 컴퓨터.  
  
2.  [보고서를 생성할](generating-reports-sybasetosql.md) 자세한 xml을 보려면 평가/변환 및 데이터 마이그레이션에 대 한 보고서를 출력 합니다. 또한 새로 고침 및 동기화 명령에 대 한 자세한 오류 보고서를 생성할 수 있습니다.  
  
## <a name="ssma-console-output-conventions"></a>SSMA 콘솔 출력 규칙  
SSMA 스크립트 명령 및 옵션을 실행할 때 콘솔 프로그램 콘솔에서 사용자에 게 결과 및 메시지 (정보, 오류 등)을 표시 또는 필요한 경우 xml 출력 파일에 리디렉션합니다. 출력에는 메시지의 각 유형에 고유한 색으로 표시 됩니다. 예를 들어 흰색 텍스트 메시지가 나타냅니다 스크립트 파일 명령을입니다. 녹색에서 하나는 사용자 입력에 대 한 프롬프트 및 등을 나타냅니다.  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
색을 해석 하는 콘솔 출력의 다음 표에 표시 됩니다.  
  
|색|설명|  
|---------|---------------|  
|빨강|실행 하는 동안 오류가 발생 했습니다|  
|회색|날짜 및 시간 스탬프를 사용자에 게 메시지|  
|하얀|스크립트 파일 명령, 메시지 유형|  
|노랑|Warning|  
|녹색|사용자 입력에 대 한 프롬프트|  
|녹청|시작, 완료 및 작업의 결과|  
  
## <a name="see-also"></a>참조  
[SAP ASE 용 SSMA 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
