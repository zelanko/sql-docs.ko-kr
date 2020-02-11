---
title: Access 용 SSMA 콘솔 시작 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8585ec16-7e0a-483a-b250-adab9b9232a3
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 899070b1405b031e919f50a6d16bc5d6df3adf3e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68222225"
---
# <a name="getting-started-with-ssma-for-access-console-accesstosql"></a>Access 용 SSMA 콘솔 시작 (AccessToSQL)
이 섹션에서는를 시작 하 고 액세스 콘솔 응용 프로그램을 시작 하는 절차에 대해 설명 합니다. 또한 여기에 나열 된 것은 일반적인 SSMA 콘솔 출력 창에서 사용 되는 규칙입니다.  
  
## <a name="launching-ssma-console"></a>SSMA 콘솔 시작  
다음 단계를 사용 하 여 SSMA 콘솔 응용 프로그램을 시작 합니다.  
  
1.  **시작** 으로 이동 하 여 **모든 프로그램**을 가리킵니다.  
  
2.  **액세스 명령 프롬프트 바로 가기에 대 한 SQL Server Migration Assistant** 를 클릭 합니다.  
  
    콘솔 응용 프로그램을 시작 하는 데 도움이 `(/? Help)`되는 ssma 콘솔 사용 메뉴가 표시 됩니다.  
  
## <a name="procedure-for-using-the-ssma-console"></a>SSMA 콘솔 사용 절차  
Windows 시스템에서 콘솔이 성공적으로 시작 된 후에는 다음 단계를 사용 하 여 작업을 수행할 수 있습니다.  
  
1.  스크립트 파일을 통해 SSMA 콘솔을 구성 합니다. 이 섹션에 대 한 자세한 내용은 [스크립트 파일 만들기 &#40;AccessToSQL&#41;](../../ssma/access/creating-script-files-accesstosql.md)를 참조 하세요.  
  
2.  [AccessToSQL&#41;&#40;변수 값 파일 만들기](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
3.  [AccessToSQL&#41;&#40;서버 연결 파일 만들기](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
4.  프로젝트 요구 사항에 따라 [AccessToSQL&#41;&#40;SSMA 콘솔 실행](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
추가 기능:  
  
1.  [암호를 지정](managing-passwords-accesstosql.md) 하 고 다른 창 컴퓨터에 내보내기/가져오기  
  
2.  평가/변환 및 데이터 마이그레이션에 대 한 자세한 xml 출력 보고서를 보려면 [보고서를 생성](generating-reports-accesstosql.md) 합니다. 새로 고침 및 동기화 명령에 대해 자세한 오류 보고서를 생성할 수도 있습니다.  
  
## <a name="ssma-console-output-conventions"></a>SSMA 콘솔 출력 규칙  
SSMA 스크립트 명령 및 옵션을 실행 하면 콘솔 프로그램이 콘솔의 사용자에 게 결과와 메시지 (정보, 오류 등)를 표시 하거나 필요한 경우 xml 출력 파일로 리디렉션합니다. 출력의 각 메시지 형식은 고유한 색으로 표시 됩니다. 예를 들어 흰색의 텍스트 메시지는 스크립트 파일 명령을 나타냅니다. 녹색으로 표시 되는 색은 사용자 입력에 대 한 프롬프트를 나타냅니다.  
  
![SSMA 콘솔 출력](../../ssma/access/media/ssmaconsoleoutput.jpg "SSMA 콘솔 출력")  
  
다음 표에서 콘솔 출력의 색 해석:  
  
|색|Description|  
|---------|---------------|  
|빨강|실행 하는 동안 심각한 오류가 발생 했습니다.|  
|회색|날짜 및 시간 스탬프, 사용자에 대 한 메시지|  
|흰색|스크립트 파일 명령, 메시지 유형|  
|노랑|Warning|  
|녹색|사용자 입력 확인|  
|녹청|작업의 시작, 종료 및 결과|  
  
## <a name="see-also"></a>참고 항목  
[액세스용 SQL Server Migration Assistant 설치](installing-sql-server-migration-assistant-for-access-accesstosql.md)  
  
