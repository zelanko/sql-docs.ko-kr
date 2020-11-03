---
description: Sybase 용 SSMA 콘솔 시작 (SybaseToSQL)
title: Sybase 용 SSMA 콘솔 시작 (SybaseToSQL) | Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 34e0a493140a31099dc4b9ed9f6234743bf0c8c1
ms.sourcegitcommit: 442fbe1655d629ecef273b02fae1beb2455a762e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93235370"
---
# <a name="getting-started-with-the-ssma-for-sybase-console-sybasetosql"></a>Sybase 용 SSMA 콘솔 시작 (SybaseToSQL)
이 섹션에서는 Sybase 콘솔 응용 프로그램용 SSMA를 시작 하 고 시작 하는 절차에 대해 설명 합니다. 또한 일반적인 SSMA 콘솔 출력 창에서 사용 되는 규칙도 여기에 나와 있습니다.  
  
## <a name="launching-the-ssma-console"></a>SSMA 콘솔 시작  
다음 단계를 사용 하 여 SSMA 콘솔 응용 프로그램을 시작 합니다.  
  
1.  시작으로 이동한 다음 모든 프로그램을 가리킵니다.  
  
2.  **Sybase 명령 프롬프트 바로 가기 SQL Server Migration Assistant를** 클릭 합니다.  
  
    콘솔 응용 프로그램을 시작 하는 데 도움이 되는 SSMA 콘솔 사용 메뉴가 표시 됩니다 `(/? Help)` .  
  
## <a name="using-the-ssma-console"></a>SSMA 콘솔 사용  
Windows 시스템에서 콘솔이 성공적으로 시작 된 후에는 다음 단계를 사용 하 여 작업을 수행할 수 있습니다.  
  
1.  스크립트 파일을 통해 SSMA 콘솔을 구성 합니다. 이 섹션에 대 한 자세한 내용은 [스크립트 파일 만들기 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md)를 참조 하세요.  
  
2.  [변수 값 파일 만들기 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [서버 연결 파일 만들기 &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [SSMA 콘솔을 실행 하는 것은 프로젝트 요구에 따라 SybaseToSQL&#41;&#40;](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) . 
  
추가 기능:  
  
1.  [암호를 지정](managing-passwords-sybasetosql.md) 하 고 다른 창 컴퓨터로 내보내고 가져옵니다.  
  
2.  [보고서를 생성](generating-reports-sybasetosql.md) 하 여 평가/변환 및 데이터 마이그레이션에 대 한 자세한 xml 출력 보고서를 확인 합니다. 새로 고침 및 동기화 명령에 대 한 자세한 오류 보고서를 생성할 수도 있습니다.  
  
## <a name="ssma-console-output-conventions"></a>SSMA 콘솔 출력 규칙  
SSMA 스크립트 명령 및 옵션을 실행 하면 콘솔 프로그램은 콘솔의 사용자에 게 결과와 메시지 (정보, 오류 등)를 표시 하거나 필요한 경우 xml 출력 파일로 리디렉션합니다. 출력의 각 메시지 형식은 고유한 색으로 표시 됩니다. 예를 들어 흰색의 텍스트 메시지는 스크립트 파일 명령을 나타냅니다. 녹색으로 표시 되는 색은 사용자 입력에 대 한 프롬프트를 나타냅니다.  
  
![SSMA 콘솔 Sybase 출력의 예를 보여 주는 스크린샷](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMA 콘솔 출력_Sybase")  
  
콘솔 출력의 색 해석을 다음 표에 표시 됩니다.  
  
|색|Description|  
|---------|---------------|  
|빨간색|실행 하는 동안 심각한 오류가 발생 했습니다.|  
|회색|날짜 및 시간 스탬프, 사용자에 대 한 메시지|  
|흰색|스크립트 파일 명령, 메시지 유형|  
|노란색|경고|  
|녹색|사용자 입력 확인|  
|녹청|작업의 시작, 종료 및 결과|  
  
## <a name="see-also"></a>참고 항목  
[SAP ASE 용 SSMA 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
