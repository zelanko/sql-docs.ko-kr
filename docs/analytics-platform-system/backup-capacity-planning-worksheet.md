---
title: 백업 서버 용량 계획 워크시트 (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: 이 용량 계획 워크시트 및 복원 작업을 SQL Server PDW 데이터베이스 백업을 수행 하기 위한 백업 서버에 대 한 요구 사항을 확인할 수 있습니다.
ms.date: 01/05/2017
ms.topic: article
ms.assetid: 36294bf6-6dde-481f-a190-d4382b04c030
caps.latest.revision: 6
ms.openlocfilehash: 1548d284f78043e5f878bafe9922480fe762dbfe
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="backup-server-capacity-planning-worksheet"></a>백업 서버 용량 계획 워크시트
이 용량 계획 워크시트 및 복원 작업을 SQL Server PDW 데이터베이스 백업을 수행 하기 위한 백업 서버에 대 한 요구 사항을 확인할 수 있습니다. 이 대화 상자를 사용 하 여 구매 새롭거나 프로 비전 기존 백업 서버에 대 한 계획을 만들 수 있습니다.  
  
이 워크시트는 명령에 보완 [를 획득 하 고 백업 서버를 구성](acquire-and-configure-backup-server.md)합니다.  
  
## <a name="capacity-planning-worksheet-for-backup-servers"></a>백업 서버에 대 한 용량 계획 워크시트  

### <a name="notes"></a>참고  
  
1.  이 워크시트는 PDW 데이터베이스에 대 한 백업 및 복원 작업을 수행 하는 서버에 적용 됩니다.  
  
2.  PDW 데이터베이스 백업 및 복원 하는 유일한 방법은 백업 데이터베이스 및 데이터베이스 SQL 복원 명령을 사용 하는 것입니다. 그러나 백업 데이터를 백업 서버에 Windows 파일의 집합으로 존재 합니다. 서버에서 백업 파일을 다른 저장소 위치로 일반적인 Windows 파일 기반 백업 방법을 포함을 사용 하 여 보관할 수 있습니다.  
  
### <a name="clipboard-iconmediaclipboard-iconpng-clipboard-icon-capacity-planning-worksheet"></a>![클립보드 아이콘](media/clipboard-icon.png "클립보드 아이콘") 용량 계획 워크시트 
  
이 워크시트를 인쇄 하 고 사용자의 요구 사항을 사용 하 여 채웁니다.  
  
|구성 요소|요구 사항|이 열을 사용자의 요구 사항 입력|권장 사항|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|저장소|지정된 된 기간 동안의 시간에 백업 서버에 저장 하려는 최대 바이트 수입니다.|![연필 아이콘](media/pencil-icon.png "연필 아이콘")|저장소 요구를 확인 하려면 시간을 지정된 된 기간에 백업 서버에 저장 하려는 데이터의 양을 파악 합니다.<br /><br />백업 데이터는 압축된 된 형식으로 백업 서버에 저장 됩니다. 데이터 압축 비율이 데이터의 특성에 따라 달라 집니다.<br /><br />예를 들어: 대략적인 예상 값으로는 7:1 압축 비율은 압축 되지 않은 데이터의 크기를 기준으로 예측 권장 합니다. 이 데이터의 80% 이상이 클러스터형된 columnstore 인덱스에 저장 된 것을 가정 합니다. 예를 들어 700 GB의 압축 되지 않은 데이터는 데이터베이스에 있는 경우 클러스터형된 columnstore 인덱스에 저장 된 다음 수 추정 데이터베이스 백업에는 약 100GB 필요 합니다.<br /><br />백업 서버에 데이터베이스 백업의 여러 복사본을 갖도록 하려는 경우를 고려해 야 합니다.<br /><br />예를 들어: 50TB의 결합 된 크기는 데이터베이스의 경우 5TB의 압축 되지 않은 데이터가 포함 된 10 개의 데이터베이스를 백업 하려는 경우. 행에 5 일에 대 한 이러한 10 개의 데이터베이스 매일 백업 하려는 경우 전체 압축 되지 않은 크기는 250 TB입니다. 7:1 압축 비율은 고려를 해야 250 / 7 = 35.7 t B의 백업 서버에 저장 합니다. 권장 되 고 실행을 가져오는 방법에 대 한 차이 해결 하 고 성장에 추가 용량을 30%입니다.  이 예제에서는 46.6 TB 더 나은 것입니다.|  
|네트워크|네트워크 연결 유형입니다.|![연필 아이콘](media/pencil-icon.png "연필 아이콘")|로드 속도 요구를 충족할 수 있는 최상의 네트워크 연결 유형을 결정 합니다.<br /><br />예를 들어: InfiniBand 또는 급여를 로드 하는 10Gbit 이더넷 최적의 제공 합니다. 1Gbit 이더넷 로드 속도를 360 GB 시간당 개 이하로 제한 합니다.|  
|입력/출력|쓰기 작업에 대해 시간당 바이트 수입니다.|![연필 아이콘](media/pencil-icon.png "연필 아이콘")|디스크에 쓰기 속도 최적의 시간당 4TB 백업을 작성 합니다.<br /><br />예를 들어: 이상 24 드라이브 원하는 50MB/sec 쓸 수 있는 드라이브에 대 한 설정 및 미러링 또는 패리티에 대해 더 합니다.<br /><br />I/O 용량에 대 한를 고려 로드 서버에서 발생 한 I/O를 모두 고려 합니다. 로드 서버에는 ETL 서버에서 데이터 파일을 받는 작업과 같은 데이터를 로드 외에도 다른 I/O 트래픽을 I/O 요구 사항이 증가 합니다.|  
|CPU|소켓의 수입니다.|![연필 아이콘](media/pencil-icon.png "연필 아이콘")|수신 및 백업 파일을 저장할 CPU를 많이 사용 응용 프로그램이 아닙니다.  최소 요구 사항으로 최근에 제조 듀얼 소켓 서버를 사용 하는 것이 좋습니다.|  
|RAM|파일을 캐시 하는 동안 Windows 수 있는 메모리를 로드 합니다.|![연필 아이콘](media/pencil-icon.png "연필 아이콘")|수신 및 백업 파일을 저장할 로드 서버의 매우 적은 양의 RAM 필요 합니다.<br /><br />RAM 요구를 확인 하려면 Windows Server 설치 및 3rd 파티 응용 프로그램 요구 사항을 가리킵니다. 다른 원본의 요구 사항이 없는 경우 32GB의 최소를 좋습니다.|  
  
용량 요구 사항을 결정 했으면 돌아가려면는 [를 획득 하 고 로드 하는 서버를 구성](acquire-and-configure-loading-server.md) 구매를 계획 하는 항목입니다.  
  
## <a name="see-also"></a>관련 항목:  
[백업 및 하드웨어를 로드 합니다.](backup-and-loading-hardware.md)  
  
