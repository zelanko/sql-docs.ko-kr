---
title: SQL Server 누적 업데이트에 대 한 CAB 다운로드
description: SQL Server 2017 Machine Learning Services 및 SQL Server 2016 R Services에 대 한 R 및 Python CAB 및 패키지 다운로드가 있습니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0fd6b624b024c51965420dd438b8eb9ec04fbafc
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344953"
---
# <a name="cab-downloads-for-cumulative-updates-of-sql-server-in-database-analytics-instances"></a>데이터베이스 내 분석 인스턴스 SQL Server의 누적 업데이트에 대 한 CAB 다운로드

데이터베이스 내 분석을 위해 구성 된 SQL Server 인스턴스에는 R 및 Python 기능이 포함 됩니다. 이러한 기능은 CAB 파일에 제공 되며 SQL Server 설치를 통해 설치 및 서비스 됩니다. 인터넷에 연결 된 장치에서 CAB 업데이트는 일반적으로 Windows 업데이트를 통해 적용 됩니다. 연결 되지 않은 서버에서는 CAB 파일을 수동으로 다운로드 하 여 적용 해야 합니다. 

이 문서에서는 각 누적 업데이트에 대 한 CAB 파일에 대 한 다운로드 링크를 제공 합니다. SQL Server 2017 Machine Learning Services (R 및 Python) 및 SQL Server 2016 R 서비스에 대 한 링크가 제공 됩니다. 오프 라인 설치에 대 한 자세한 내용은 [인터넷에 액세스 하지 않고 machine learning 구성 요소 설치 SQL Server](sql-ml-component-install-without-internet-access.md#apply-cu)를 참조 하세요.

## <a name="prerequisites"></a>사전 요구 사항

기준 설치를 시작 합니다.

+ SQL Server 2017 Machine Learning Services에서 초기 릴리스는 기본 설치입니다. 
+ SQL Server 2016 R Services에서 초기 릴리스, SP1 또는 s p 2로 시작할 수 있습니다. 

또한 독립 실행형 서버에 누적 업데이트를 적용할 수 있습니다.

## <a name="sql-server-2017-cabs"></a>SQL Server 2017 CABs

CAB 파일은 역순 시간 순서로 나열 됩니다. CAB 파일을 다운로드 하 여 대상 컴퓨터에 전송 하는 경우 **다운로드** 또는 설치 사용자의% temp% 폴더와 같은 편리한 폴더에 저장 합니다.

|릴리스  |구성 요소 | 다운로드 링크  | 해결 된 문제 | 
|---------|----------|----------------|------------------|
|**[SQL Server 2017 CU14](https://support.microsoft.com/help/4484710/)-[CU15](https://support.microsoft.com/help/4498951/)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073898&clcid=1033)| 패키지 내의 이진 파일은 이제 서명 됩니다. |
| | R Server      |[SRS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2069739&clcid=1033)| 패키지 내의 이진 파일은 이제 서명 됩니다. |
| | Microsoft Python Open     | [SPO_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073897&clcid=1033)| 패키지 내의 이진 파일은 이제 서명 됩니다. |
| | Python Server    |[SPS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2071421&clcid=1033)| 패키지 내의 이진 파일은 이제 서명 됩니다.  |
|**[SQL Server 2017 CU13](https://support.microsoft.com/help/4466404)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 이전 버전에서 변경 되지 않았습니다. |
| | R Server      |[SRS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038263&clcid=1033)| 에는 SQL Server 설치 프로그램을 통해 설치 된 [조작 가능한 독립 실행형 R Server](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)를 업그레이드 하는 방법이 포함 되어 있습니다. CU13 Cab를 사용 하 고 [다음 지침](sql-machine-learning-standalone-windows-install.md#apply-cu) 에 따라 업데이트를 적용 합니다. |
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 이전 버전에서 변경 되지 않았습니다. |
| | Python Server    |[SPS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038197&clcid=1033)| SQL Server 설치 프로그램을 통해 설치 되는 [조작 가능한 독립 실행형 Python 서버](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)를 업그레이드 하는 방법에 대 한 수정 사항이 포함 되어 있습니다. CU13 Cab를 사용 하 고 [다음 지침](sql-machine-learning-standalone-windows-install.md#apply-cu) 에 따라 업데이트를 적용 합니다. |
|**[SQL Server 2017 CU10](https://support.microsoft.com/help/4342123)-[CU11](https://support.microsoft.com/help/4462262)-[CU12](https://support.microsoft.com/help/4464082)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 이전 버전에서 변경 되지 않았습니다. |
| | R Server      |[SRS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006287&clcid=1033)| 사소한 수정입니다.|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 이전 버전에서 변경 되지 않았습니다. |
| | Python Server    |[SPS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006805&clcid=1033)| 중복 항목을 제거 하면 Python rx_data_step에서 행 순서를 잃게 됩니다. <br/>SPEE는 클러스터형 columnstore 인덱스에서 데이터 형식 검색에 실패 합니다. <br/>열에 모든 null 값이 포함 된 경우 빈 테이블을 반환 합니다. |
|**[SQL Server 2017 CU8](https://support.microsoft.com/help/4338363)-[CU9](https://support.microsoft.com/help/4341265)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 이전 버전에서 변경 되지 않았습니다. |
| | R Server      |[SRS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874708&clcid=1033)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 이전 버전에서 변경 되지 않았습니다. |
| | Python Server    |[SPS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874707&clcid=1033)|
|**[SQL Server 2017 CU6](https://support.microsoft.com/help/4101464)-[CU7](https://support.microsoft.com/help/4229789)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 이전 버전에서 변경 되지 않았습니다. |
| | R Server      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 이전 버전에서 변경 되지 않았습니다. |
| | Python Server    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)| SPEES 쿼리의 DateTime 데이터 형식입니다.<br/>미리 학습 된 모델이 없는 경우 microsoftml의 오류 메시지가 개선 되었습니다.<br/> Revoscalepy 변환 함수 및 변수를 수정 합니다.|
|**[SQL Server 2017 CU5](https://support.microsoft.com/help/4092643)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 이전 버전에서 변경 되지 않았습니다. |
| | R Server      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)| RxInstallPackages의 긴 경로 관련 오류입니다.<br/>RxExec에 대 한 루프백의 연결
| | Microsoft Python Open    | 이전 버전에서 변경 되지 않았습니다. |
| | Python Server    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)| <br/>Rx_exec에 대 한 루프백의 연결
|**[SQL Server 2017 CU4](https://support.microsoft.com/help/4056498)** |  |   |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 이전 버전에서 변경 되지 않았습니다. |
| | R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 이전 버전에서 변경 되지 않았습니다. |
| |  Python Server    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
|**[SQL Server 2017 CU3](https://support.microsoft.com/help/4052987)** |  |  |  |
| | Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
| | R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 이전 버전에서 변경 되지 않았습니다. |
| | Python Server    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)| [Rx_serialize_model 함수](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)를 사용 하 여 revoscalepy의 Python 모델 serialization.<br/>[기본 점수 매기기](../sql-native-scoring.md) 지원과 [실시간 점수 매기기](../real-time-scoring.md)기능이 향상 되었습니다. 
|**[SQL Server 2017 CU1](https://support.microsoft.com/help/4038634)-[CU2](https://support.microsoft.com/help/4052574)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)| 이전 버전에서 변경 되지 않았습니다. |
| | R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 이전 버전에서 변경 되지 않았습니다. | 
| | Python Server    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) | 스키마 정보를 반환 하기 위한 rx_create_col_info를 추가 합니다. <br/>`RxLocalParallel` 계산 컨텍스트를 사용 하 여 병렬 시나리오를 지원 하기 위한 [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) 향상|
|**초기 릴리스** |  |  |
| | Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
| | R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
| | Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |


<a name="bkmk_2016Installers"></a>

## <a name="sql-server-2016-cabs"></a>SQL Server 2016 CABs

SQL Server 2016 R Services의 경우 기본 릴리스는 RTM 버전 또는 Service Pack 버전입니다.

|릴리스  |다운로드 링크  |
|---------|---------------|
|**SQL Server 2016 SP2 CU6**     |
|Microsoft R Open     |[SRO_3.2.2.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079936&clcid=1033)|
|Microsoft R Server    |[SRS_8.0.3.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079933&clcid=1033)|
|**SQL Server 2016 SP2 CU1-CU5**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038)|
|**SQL Server 2016 SP2**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)|
|**SQL Server 2016 SP1 CU14**     |
|Microsoft R Open     |[SRO_3.2.2.16100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2080130&clcid=1033)|
|Microsoft R Server    |[SRS_8.0.3.17200_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079935&clcid=1033)|
|**SQL Server 2016 SP1 CU1-CU13**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
|**SQL Server 2016 SP1**     |
|Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)|
|Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)|
|**SQL Server 2016 CU4-CU9**     |
|Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
|Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
|**SQL Server 2016 CU2-CU3**     |
|Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)|
|Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)|
|**SQL Server 2016 CU1**     |
|Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)|
|Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)|
|**SQL Server 2016 RTM**     |
|Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)|
|Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)|

> [!NOTE]
> 
> SQL Server 2016 SP1 CU4 또는 SP1 CU5 offline을 설치 하는 경우 SRO_ 3.2.2.16000 _1033.cab를 다운로드 합니다. 설치 대화 상자에 표시 된 것 처럼 FWLINK 831785에서 SRO_ 3.2.2.13000 _1033.cab를 다운로드 한 경우 누적 업데이트를 설치 하기 전에 파일 이름을 SRO_ 3.2.2.16000 _1033.cab로 바꿉니다.

Microsoft R에 대 한 소스 코드를 보려면 다음을 사용 하 여 파일을. tar 형식으로 다운로드할 수 있습니다. [R Server 설치 관리자 다운로드](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

## <a name="see-also"></a>참조

[인터넷에 액세스 하지 않고 컴퓨터에 누적 업데이트 적용](sql-ml-component-install-without-internet-access.md#apply-cu)

[인터넷에 연결 되어 있는 컴퓨터에 누적 업데이트 적용](sql-ml-component-install-without-internet-access.md#apply-cu)

[독립 실행형 서버에 누적 업데이트 적용](sql-machine-learning-standalone-windows-install.md#apply-cu)
