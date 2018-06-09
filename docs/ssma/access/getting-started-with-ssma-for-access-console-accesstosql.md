---
title: 액세스 콘솔 (AccessToSQL) 용 SSMA 시작 | Microsoft Docs
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
ms.assetid: 8585ec16-7e0a-483a-b250-adab9b9232a3
caps.latest.revision: 21
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c37a486c560a5dc0cb6298f93b4486accc18354b
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34773919"
---
# <a name="getting-started-with-ssma-for-access-console-accesstosql"></a>액세스 콘솔 (AccessToSQL) 용 SSMA 시작
이 섹션에서는 시작 하 고 액세스 콘솔 응용 프로그램을 시작 하는 절차를 설명 합니다. 또한 나열 된 여기에 규칙이 사용 일반적인 SSMA 콘솔 출력 창에.  
  
## <a name="launching-ssma-console"></a>SSMA 콘솔 시작  
SSMA 콘솔 응용 프로그램을 시작 하려면 다음 단계를 사용 합니다.  
  
1.  로 이동 **시작** 를 가리키도록 **모든 프로그램**합니다.  
  
2.  클릭는 **SQL Server Migration Assistant 액세스 명령 프롬프트에 대 한** 바로 가기 합니다.  
  
    SSMA 콘솔 사용 메뉴를 표시 하 고 `(/? Help)`, 콘솔 응용 프로그램을 시작할 수 있도록 합니다.  
  
## <a name="procedure-for-using-the-ssma-console"></a>SSMA 콘솔을 사용 하기 위한 절차  
Windows 시스템에 콘솔이 성공적으로 시작 후에 작업을 다음 단계를 사용할 수 있습니다.  
  
1.  SSMA 콘솔 스크립트 파일을 통해 구성 합니다. 이 섹션에 대 한 자세한 내용은 참조 하십시오. [스크립트 파일 만들기 &#40;AccessToSQL&#41;](../../ssma/access/creating-script-files-accesstosql.md)합니다.  
  
2.  [변수 값 파일을 만드는 &#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
3.  [서버 연결 파일 만들기 &#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
4.  [SSMA 콘솔 실행 &#40;AccessToSQL&#41; ](../../ssma/access/executing-the-ssma-console-accesstosql.md) 프로젝트 요구 사항에 따라  
  
추가 기능:  
  
1.  [암호를 지정](http://msdn.microsoft.com/en-us/b099d0f9-dd37-4c87-8b6f-ed0177881ea4) 다른 창 컴퓨터 가져오기 / 내보내기 하 고  
  
2.  [보고서를 생성할](http://msdn.microsoft.com/en-us/abb4264a-622e-4215-af5b-14e309b8a399) 자세한 xml을 보려면 평가 /conversion 및 데이터 마이그레이션에 대 한 보고서를 출력 합니다. 새로 고침 및 동기화 명령에 대 한 자세한 오류 보고서를 생성할 수도 있습니다.  
  
## <a name="ssma-console-output-conventions"></a>SSMA 콘솔 출력 규칙  
SSMA 스크립트 명령 및 옵션을 실행 결과 및 메시지 (정보, 오류 등)를 콘솔에 표시 하는 콘솔 프로그램 만들거나 필요한 경우 xml 출력 파일로 리디렉션합니다. 각 유형의 메시지 출력에는 고유한 색으로 표시 됩니다. 예를 들어 흰색에 문자 메시지가 나타냅니다 스크립트 파일 명령을입니다. 녹색의 사용자 입력에 대 한 프롬프트 및 등을 나타냅니다.  
  
![SSMA 콘솔 출력](../../ssma/access/media/ssmaconsoleoutput.jpg "SSMA 콘솔 출력")  
  
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
[SQL Server Migration Assistant for Access 설치](http://msdn.microsoft.com/en-us/dd50eebd-75df-4e0d-8c4d-88b511aae4c7)  
  
