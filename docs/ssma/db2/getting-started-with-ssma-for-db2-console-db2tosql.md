---
title: DB2 콘솔 (DB2ToSQL) 용 SSMA 시작 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f245c017-023e-4880-8721-8908d339525e
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3b8417d75ab0a08532dd073b3ce7f803b3f7490c
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51668302"
---
# <a name="getting-started-with-ssma--for-db2-console-db2tosql"></a>DB2 콘솔 (DB2ToSQL) 용 SSMA 시작
이 섹션에서는 시작 하 고 DB2 콘솔 응용 프로그램을 시작 하는 절차를 설명 합니다. 도 나열 여기에 규칙에에서 사용 됩니다 일반적인 SSMA 콘솔 출력 창.  
  
## <a name="launching-ssma-console"></a>SSMA 콘솔 시작  
SSMA 콘솔 응용 프로그램을 시작 하려면 다음 단계를 사용 합니다.  
  
1.  로 이동 **시작** 가리킨 **프로그램도**합니다.  
  
2.  클릭 합니다  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant DB2 명령 프롬프트에 대 한** 바로 가기.  
  
    SSMA 콘솔 사용 메뉴 표시 및 `(/? Help)`콘솔 응용 프로그램을 시작할 수 있도록 합니다.  
  
## <a name="procedure-for-using-the-ssma-console"></a>SSMA 콘솔을 사용 하는 절차  
콘솔 Windows 시스템에 성공적으로 시작 되 면 다음 단계에 작업을 사용할 수 있습니다.  
  
1.  SSMA 콘솔 스크립트 파일을 통해 구성 합니다. 이 섹션에 대 한 자세한 내용은 참조 하세요. [스크립트 파일 만들기 &#40;DB2ToSQL&#41; ](../../ssma/db2/creating-script-files-db2tosql.md) 합니다.  
  
2.  [변수 값 파일 만들기 &#40;DB2ToSQL&#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
  
3.  [서버 연결 파일 만들기 &#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
4.  [SSMA 콘솔 실행 &#40;DB2ToSQL&#41; ](../../ssma/db2/executing-the-ssma-console-db2tosql.md) 프로젝트 요구 사항에 따라  
  
추가 기능:  
  
1.  [암호 관리](https://msdn.microsoft.com/56d546e3-8747-4169-aace-693302667e94) 다른 창 컴퓨터 가져오기 / 내보내기 하 고  
  
2.  [보고서 생성](https://msdn.microsoft.com/69ef5fd9-190d-4c58-8199-b3f77d5e1883) 자세한 xml을 보려면 평가 /conversion 및 데이터 마이그레이션에 대 한 보고서를 출력 합니다. 새로 고침 및 동기화 명령에 대 한 자세한 오류 보고서를 생성할 수도 있습니다.  
  
## <a name="ssma-console-output-conventions"></a>SSMA 콘솔 출력 규칙  
SSMA 스크립트 명령 및 옵션을 실행할 때 콘솔 프로그램 콘솔에서 사용자에 게 결과 및 메시지 (정보, 오류 등)을 표시 또는 필요한 경우 xml 출력 파일에 리디렉션합니다. 출력에는 메시지의 각 유형에 고유한 색으로 표시 됩니다. 예를 들어 흰색 텍스트 메시지가 나타냅니다 스크립트 파일 명령을입니다. 녹색에서 하나는 사용자 입력에 대 한 프롬프트 및 등을 나타냅니다.  
  
![SSMA 콘솔 Output_Oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "SSMA 콘솔 Output_Oracle")  
  
다음 표에서 콘솔 출력의 색을 해석:  
  
|색|설명|  
|---------|---------------|  
|빨강|실행 하는 동안 오류가 발생 했습니다|  
|회색|날짜 및 시간 스탬프를 사용자에 게 메시지|  
|흰색|스크립트 파일 명령, 메시지 유형|  
|노란색|경고|  
|녹색|사용자 입력에 대 한 프롬프트|  
|녹청|시작을 완료 하 고 작업의 결과|  
  
## <a name="see-also"></a>관련 항목  
[DB2 용 SSMA 설치](https://msdn.microsoft.com/79fbe8ea-471b-407a-be2a-4100d9b57c61)  
  
