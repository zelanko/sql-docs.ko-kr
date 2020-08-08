---
title: DB2 용 SSMA 콘솔 시작 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f245c017-023e-4880-8721-8908d339525e
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 17798a2ccc0099210874a4bebb4fd05074c43639
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87933874"
---
# <a name="getting-started-with-ssma--for-db2-console-db2tosql"></a>DB2 용 SSMA 콘솔 시작 (DB2ToSQL)
이 섹션에서는 DB2 콘솔 응용 프로그램을 시작 하 고 시작 하는 절차에 대해 설명 합니다. 또한 여기에 나열 된 것은 일반적인 SSMA 콘솔 출력 창에서 사용 되는 규칙입니다.  
  
## <a name="launching-ssma-console"></a>SSMA 콘솔 시작  
다음 단계를 사용 하 여 SSMA 콘솔 응용 프로그램을 시작 합니다.  
  
1.  **시작** 으로 이동 하 여 **모든 프로그램**을 가리킵니다.  
  
2.  ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB2 용 Migration Assistant 명령 프롬프트** 바로 가기를 클릭 합니다.  
  
    콘솔 응용 프로그램을 시작 하는 데 도움이 되는 SSMA 콘솔 사용 메뉴가 표시 됩니다 `(/? Help)` .  
  
## <a name="procedure-for-using-the-ssma-console"></a>SSMA 콘솔 사용 절차  
Windows 시스템에서 콘솔이 성공적으로 시작 된 후에는 다음 단계를 사용 하 여 작업을 수행할 수 있습니다.  
  
1.  스크립트 파일을 통해 SSMA 콘솔을 구성 합니다. 이 섹션에 대 한 자세한 내용은 [스크립트 파일 만들기 &#40;DB2ToSQL&#41;](../../ssma/db2/creating-script-files-db2tosql.md) 를 참조 하세요.  
  
2.  [DB2ToSQL&#41;&#40;변수 값 파일 만들기](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
  
3.  [DB2ToSQL&#41;&#40;서버 연결 파일 만들기](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
4.  프로젝트 요구 사항에 따라 [DB2ToSQL&#41;&#40;SSMA 콘솔 실행](../../ssma/db2/executing-the-ssma-console-db2tosql.md)  
  
추가 기능:  
  
1.  [암호 관리](https://msdn.microsoft.com/56d546e3-8747-4169-aace-693302667e94) 및 다른 창 컴퓨터로 내보내기/가져오기  
  
2.  평가/변환 및 데이터 마이그레이션에 대 한 자세한 xml 출력 보고서를 볼 수 있는 [보고서를 생성](https://msdn.microsoft.com/69ef5fd9-190d-4c58-8199-b3f77d5e1883) 합니다. 새로 고침 및 동기화 명령에 대해 자세한 오류 보고서를 생성할 수도 있습니다.  
  
## <a name="ssma-console-output-conventions"></a>SSMA 콘솔 출력 규칙  
SSMA 스크립트 명령 및 옵션을 실행 하면 콘솔 프로그램이 콘솔의 사용자에 게 결과와 메시지 (정보, 오류 등)를 표시 하거나 필요한 경우 xml 출력 파일로 리디렉션합니다. 출력의 각 메시지 형식은 고유한 색으로 표시 됩니다. 예를 들어 흰색의 텍스트 메시지는 스크립트 파일 명령을 나타냅니다. 녹색으로 표시 되는 색은 사용자 입력에 대 한 프롬프트를 나타냅니다.  
  
![SSMA 콘솔 출력_Oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "SSMA 콘솔 출력_Oracle")  
  
다음 표에서 콘솔 출력의 색 해석:  
  
|색|Description|  
|---------|---------------|  
|빨간색|실행 하는 동안 심각한 오류가 발생 했습니다.|  
|회색|날짜 및 시간 스탬프, 사용자에 대 한 메시지|  
|흰색|스크립트 파일 명령, 메시지 유형|  
|노란색|경고|  
|녹색|사용자 입력 확인|  
|녹청|작업의 시작, 종료 및 결과|  
  
## <a name="see-also"></a>참고 항목  
[D b 2 용 SSMA 설치](https://msdn.microsoft.com/79fbe8ea-471b-407a-be2a-4100d9b57c61)  
  
