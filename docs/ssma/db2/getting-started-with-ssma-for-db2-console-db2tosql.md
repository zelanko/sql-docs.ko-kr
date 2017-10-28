---
title: "DB2 콘솔 (DB2ToSQL) 용 SSMA 시작 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: f245c017-023e-4880-8721-8908d339525e
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 24c96c6e76d89d271d80e3be51c8c27d62dbd6b3
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="getting-started-with-ssma--for-db2-console-db2tosql"></a>DB2 콘솔 (DB2ToSQL) 용 SSMA 시작
이 섹션에서는 시작 하 고 DB2 콘솔 응용 프로그램을 시작 하는 절차를 설명 합니다. 또한 나열 된 여기에 규칙이 사용 일반적인 SSMA 콘솔 출력 창에.  
  
## <a name="launching-ssma-console"></a>SSMA 콘솔 시작  
SSMA 콘솔 응용 프로그램을 시작 하려면 다음 단계를 사용 합니다.  
  
1.  로 이동 **시작** 를 가리키도록 **모든 프로그램**합니다.  
  
2.  클릭는  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant DB2 명령 프롬프트에 대 한** 바로 가기 합니다.  
  
    SSMA 콘솔 사용 메뉴를 표시 하 고 `(/? Help)`, 콘솔 응용 프로그램을 시작할 수 있도록 합니다.  
  
## <a name="procedure-for-using-the-ssma-console"></a>SSMA 콘솔을 사용 하기 위한 절차  
Windows 시스템에 콘솔이 성공적으로 시작 후에 작업을 다음 단계를 사용할 수 있습니다.  
  
1.  SSMA 콘솔 스크립트 파일을 통해 구성 합니다. 이 섹션에 대 한 자세한 내용은 참조 하십시오. [스크립트 파일 만들기 &#40; DB2ToSQL &#41;](../../ssma/db2/creating-script-files-db2tosql.md) 합니다.  
  
2.  [만드는 변수 값 파일 &#40; DB2ToSQL &#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
  
3.  [서버 연결 파일 &#40; DB2ToSQL &#41; 만들기](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
4.  [SSMA 콘솔 &#40; DB2ToSQL &#41;를 실행합니다. ](../../ssma/db2/executing-the-ssma-console-db2tosql.md) 프로젝트 요구 사항에 따라  
  
추가 기능:  
  
1.  [암호 관리](http://msdn.microsoft.com/en-us/56d546e3-8747-4169-aace-693302667e94) 다른 창 컴퓨터 가져오기 / 내보내기 하 고  
  
2.  [보고서 생성](http://msdn.microsoft.com/en-us/69ef5fd9-190d-4c58-8199-b3f77d5e1883) 자세한 xml을 보려면 평가 /conversion 및 데이터 마이그레이션에 대 한 보고서를 출력 합니다. 새로 고침 및 동기화 명령에 대 한 자세한 오류 보고서를 생성할 수도 있습니다.  
  
## <a name="ssma-console-output-conventions"></a>SSMA 콘솔 출력 규칙  
SSMA 스크립트 명령 및 옵션을 실행 결과 및 메시지 (정보, 오류 등)를 콘솔에 표시 하는 콘솔 프로그램 만들거나 필요한 경우 xml 출력 파일로 리디렉션합니다. 각 유형의 메시지 출력에는 고유한 색으로 표시 됩니다. 예를 들어 흰색에 문자 메시지가 나타냅니다 스크립트 파일 명령을입니다. 녹색의 사용자 입력에 대 한 프롬프트 및 등을 나타냅니다.  
  
![SSMA 콘솔 Output_Oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "SSMA 콘솔 Output_Oracle")  
  
다음 표에서 콘솔 출력의 색을 해석:  
  
|색|Description|  
|---------|---------------|  
|빨강|실행 하는 동안 심각한 오류|  
|회색|날짜 및 시간 스탬프를 사용자에 게 메시지|  
|흰색|스크립트 파일 명령, 메시지 유형|  
|노란색|경고|  
|녹색|사용자 입력에 대 한 프롬프트|  
|녹청|시작, 완료 및 작업의 결과|  
  
## <a name="see-also"></a>관련 항목:  
[D b 2 용 SSMA를 설치합니다.](http://msdn.microsoft.com/en-us/79fbe8ea-471b-407a-be2a-4100d9b57c61)  
  

