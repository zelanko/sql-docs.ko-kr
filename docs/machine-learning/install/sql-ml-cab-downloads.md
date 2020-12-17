---
title: 오프라인 설치를 위한 업데이트 CAB 다운로드
description: SQL Server Machine Learning Services용 Python 및 R CAB 파일을 다운로드합니다. 이러한 CAB 파일은 Machine Learning Services(Python 및 R) 기능에 대한 업데이트를 포함하며 인터넷에 액세스할 수 없는 서버에 SQL Server를 설치할 때 사용됩니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/02/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: a356a006e2defb8fd8c99f479280ff75c5ea45d9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471164"
---
# <a name="cab-downloads-for-offline-installation-of-cumulative-updates-for-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services에 대한 누적 업데이트의 오프라인 설치를 위한 CAB 다운로드

[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

::: moniker range=">=sql-server-2017"
SQL Server Machine Learning Services용 Python 및 R CAB 파일을 다운로드합니다. 이러한 CAB 파일은 Machine Learning Services(Python 및 R) 기능에 대한 업데이트를 포함하며 인터넷에 액세스할 수 없는 서버에 SQL Server를 설치할 때 사용됩니다.
::: moniker-end

::: moniker range="=sql-server-2016"
SQL Server 2016 R Services용 Python 및 R CAB 파일을 다운로드합니다. 이러한 CAB 파일은 R Services 기능에 대한 업데이트를 포함하며 인터넷에 액세스할 수 없는 서버에 SQL Server를 설치할 때 사용됩니다.
::: moniker-end

각 누적 업데이트에 대한 CAB 파일 다운로드 링크들은 아래와 같습니다. 오프라인 설치에 대한 자세한 내용은 [인터넷 액세스 없이 SQL Server Machine Learning 구성 요소 설치](sql-ml-component-install-without-internet-access.md#apply-cu)를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

::: moniker range=">=sql-server-2017"
기본 설치로 시작합니다. SQL Server Machine Learning Services에서 초기 릴리스가 기본 설치입니다. 
::: moniker-end

::: moniker range="=sql-server-2016"
기본 설치로 시작합니다.  SQL Server 2016 R Services에서는 초기 릴리스, SP1 또는 SP2로 시작할 수 있습니다. 
::: moniker-end

누적 업데이트를 적용할 수도 있습니다.

::: moniker range="=sql-server-ver15"

## <a name="sql-server-2019-cabs"></a>SQL Server 2019 CAB

CAB 파일은 시간의 역순으로 나열됩니다. CAB 파일을 다운로드하고 이를 대상 컴퓨터로 전송할 때는 **Downloads** 또는 설치 프로그램 사용자의 %temp% 폴더와 같은 편리한 폴더에 배치합니다.

|해제 | 구성 요소 | 다운로드 링크 | 해결된 문제 |
|------- | --------- | ------------- | ---------------- |
|**[SQL Server 2019 CU8](https://support.microsoft.com/help/4577194)** |  |  |  |
| | Microsoft R Open      | [SRO_3.5.2.777_1033.cab](https://go.microsoft.com/fwlink/?linkid=2134897)  |  |
| | R Server              | [SRS_9.4.7.958_1033.cab](https://go.microsoft.com/fwlink/?linkid=2136942)  |  |
| | Microsoft Python Open | [SPO_4.5.12.479_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2118341) |  |
| | Python 서버         | [SPS_9.4.7.958_1033.cab](https://go.microsoft.com/fwlink/?linkid=2136731)  |  |
|**[SQL Server 2019 CU5](https://support.microsoft.com/help/4552255)** |  |  |  |
| | Microsoft R Open      | [SRO_3.5.2.293_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2118178)  |  |
| | R Server              | [SRS_9.4.7.804_1033.cab](https://go.microsoft.com/fwlink/?linkid=2122004)  |  |
| | Microsoft Python Open | [SPO_4.5.12.479_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2118341) |  |
| | Python 서버         | [SPS_9.4.7.804_1033.cab](https://go.microsoft.com/fwlink/?linkid=2121809)  |  |
|**[SQL Server 2019 CU3](https://support.microsoft.com/help/4538853)** |  |  |  |
| | Microsoft R Open      | [SRO_3.5.2.293_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2118178)  |  |
| | R Server              | [SRS_9.4.7.717_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2118177)  |  |
| | Microsoft Python Open | [SPO_4.5.12.479_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2118341) |  |
| | Python 서버         | [SPS_9.4.7.717_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2118342)  |  |
|**[SQL Server 2019 CU2](https://support.microsoft.com/help/4536075)** |  |  |  |
| | Microsoft R Open      | [SRO_3.5.2.125_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2085686)  |  |
| | R Server              | [SRS_9.4.7.35_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2113250)   |  |
| | Microsoft Python Open | [SPO_4.5.12.692_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2113303) |  |
| | Python 서버         | [SPS_9.4.7.35_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2113067)   |  |
|**[SQL Server 2019 CU1](https://support.microsoft.com/help/4527376)** |  |  |  |
| | Microsoft R Open      | [SRO_3.5.2.125_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2085686)  |  |
| | R Server              | [SRS_9.4.7.25_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2085792)   |  |
| | Microsoft Python Open | [SPO_4.5.12.120_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2085793) |  |
| | Python 서버         | [SPS_9.4.7.25_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2085685)   |  |
|**초기 릴리스** | | | |
| | Microsoft R Open       | [SRO_3.5.2.125_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085686)  |  |
| | R Server               | [SRS_9.4.7.25_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085792)|   |  |
| | Microsoft Python Open  | [SPO_4.5.12.120_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085793) |  |
| | Python 서버          | [SPS_9.4.7.25_1033.cab](https://go.microsoft.com/fwlink/?linkid=2085685)   |  |

::: moniker-end

::: moniker range="=sql-server-2017"

## <a name="sql-server-2017-cabs"></a>SQL Server 2017 CAB

CAB 파일은 시간의 역순으로 나열됩니다. CAB 파일을 다운로드하고 이를 대상 컴퓨터로 전송할 때는 **Downloads** 또는 설치 프로그램 사용자의 %temp% 폴더와 같은 편리한 폴더에 배치합니다.

|해제  |구성 요소 | 다운로드 링크  | 해결된 문제 | 
|---------|----------|----------------|------------------|
|**[SQL Server 2017 CU22](https://support.microsoft.com/help/4577467/)** |  |  |  |
| | Microsoft R Open      | [SRO_3.5.2.777_1033.cab](https://go.microsoft.com/fwlink/?linkid=2134897)  |  |
| | R Server              | [SRS_9.4.7.958_1033.cab](https://go.microsoft.com/fwlink/?linkid=2136942)  |  |
| | Microsoft Python Open | [SPO_4.5.12.479_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2118341) |  |
| | Python 서버         | [SPS_9.4.7.958_1033.cab](https://go.microsoft.com/fwlink/?linkid=2136731)  |  |
|**[SQL Server 2017 CU19](https://support.microsoft.com/help/4535007/)-[CU20](https://support.microsoft.com/help/4541283/)** |  |  |  |
| | Microsoft R Open | [SRO_3.3.3.1900_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2106367&clcid=1033) | R 스크립트를 실행하는 `sp_execute_external_script`에서 경고 메시지를 표시하는 버그를 수정합니다. |
| | R Server| [SRS_9.2.0.1900_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2106460&clcid=1033) | 이전 버전과의 변경 사항이 없습니다. |
| | Microsoft Python Open | [SPO_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073897&clcid=1033) | 이전 버전과의 변경 사항이 없습니다. |
| | Python 서버 | [SPS_9.2.0.1900_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2106459&clcid=1033) | python 스크립트를 실행하는 `sp_execute_external_script`가 varbinary 또는 이진 데이터 형식을 OutputDataSet 형식으로 SQL Server에 다시 반환할 때 때때로 데이터가 손실되는 버그를 수정합니다. |
|**[SQL Server 2017 CU14](https://support.microsoft.com/help/4484710/)-[CU15](https://support.microsoft.com/help/4498951/)-[CU16](https://support.microsoft.com/help/4508218/)-[CU17](https://support.microsoft.com/help/4515579/)-[CU18](https://support.microsoft.com/help/4527377/)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073898&clcid=1033)| 패키지 내의 이진 파일이 이제 서명된 상태입니다. |
| | R Server      |[SRS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2069739&clcid=1033)| 패키지 내의 이진 파일이 이제 서명된 상태입니다. |
| | Microsoft Python Open     | [SPO_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073897&clcid=1033)| 패키지 내의 이진 파일이 이제 서명된 상태입니다. |
| | Python 서버    |[SPS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2071421&clcid=1033)| 패키지 내의 이진 파일이 이제 서명된 상태입니다.  |
|**[SQL Server 2017 CU13](https://support.microsoft.com/help/4466404)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 이전 버전과의 변경 사항이 없습니다. |
| | R Server      |[SRS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038263&clcid=1033)| SQL Server 설치 프로그램을 통해 설치될 때와 같이 [운영화된 독립형 R 서버](/machine-learning-server/what-is-operationalization)를 업그레이드하기 위한 수정이 포함되어 있습니다. CU13 CAB를 사용하고 [해당 지침](sql-machine-learning-standalone-windows-install.md#apply-cu)에 따라 업데이트를 적용합니다. |
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 이전 버전과의 변경 사항이 없습니다. |
| | Python 서버    |[SPS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038197&clcid=1033)| SQL Server 설치 프로그램을 통해 설치될 때와 같이 [운영화된 독립형 Python 서버](/machine-learning-server/what-is-operationalization)를 업그레이드하기 위한 수정이 포함되어 있습니다. CU13 CAB를 사용하고 [해당 지침](sql-machine-learning-standalone-windows-install.md#apply-cu)에 따라 업데이트를 적용합니다. |
|**[SQL Server 2017 CU10](https://support.microsoft.com/help/4342123)-[CU11](https://support.microsoft.com/help/4462262)-[CU12](https://support.microsoft.com/help/4464082)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 이전 버전과의 변경 사항이 없습니다. |
| | R Server      |[SRS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006287&clcid=1033)| 사소한 수정입니다.|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 이전 버전과의 변경 사항이 없습니다. |
| | Python 서버    |[SPS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006805&clcid=1033)| 중복 항목을 제거하면 Python rx_data_step의 행 순서가 손실됩니다. <br/>클러스터형 columnstore 인덱스에서 SPEE의 데이터 형식 감지가 실패합니다. <br/>열에 모두 null 값이 포함된 경우 빈 테이블을 반환합니다. |
|**[SQL Server 2017 CU8](https://support.microsoft.com/help/4338363)-[CU9](https://support.microsoft.com/help/4341265)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 이전 버전과의 변경 사항이 없습니다. |
| | R Server      |[SRS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874708&clcid=1033)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 이전 버전과의 변경 사항이 없습니다. |
| | Python 서버    |[SPS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874707&clcid=1033)|
|**[SQL Server 2017 CU6](https://support.microsoft.com/help/4101464)-[CU7](https://support.microsoft.com/help/4229789)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 이전 버전과의 변경 사항이 없습니다. |
| | R Server      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 이전 버전과의 변경 사항이 없습니다. |
| | Python 서버    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)| SPEES 쿼리의 DateTime 데이터 형식입니다.<br/>사전 학습된 모델이 누락된 경우 microsoftml에 향상된 오류 메시지가 표시됩니다.<br/> revoscalepy 변환 함수 및 변수가 수정되었습니다.|
|**[SQL Server 2017 CU5](https://support.microsoft.com/help/4092643)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 이전 버전과의 변경 사항이 없습니다. |
| | R Server      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)| rxInstallPackages에 긴 경로 관련 오류가 있습니다.<br/>RxExec를 위한 루프백 연결입니다.
| | Microsoft Python Open    | 이전 버전과의 변경 사항이 없습니다. |
| | Python 서버    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)| <br/>rx_exec를 위한 루프백 연결입니다.
|**[SQL Server 2017 CU4](https://support.microsoft.com/help/4056498)** |  |   |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 이전 버전과의 변경 사항이 없습니다. |
| | R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 이전 버전과의 변경 사항이 없습니다. |
| |  Python 서버    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
|**[SQL Server 2017 CU3](https://support.microsoft.com/help/4052987)** |  |  |  |
| | Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
| | R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 이전 버전과의 변경 사항이 없습니다. |
| | Python 서버    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)| [rx_serialize_model function](/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)를 사용하는 revoscalepy의 Python 모델 직렬화입니다.<br/>[실시간 채점](../predictions/real-time-scoring.md)에대 한 향상 기능과 함께 [네이티브 채점](../predictions/native-scoring-predict-transact-sql.md)을 지원합니다. 
|**[SQL Server 2017 CU1](https://support.microsoft.com/help/4038634)-[CU2](https://support.microsoft.com/help/4052574)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)| 이전 버전과의 변경 사항이 없습니다. |
| | R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 이전 버전과의 변경 사항이 없습니다. | 
| | Python 서버    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) | 스키마 정보를 반환하기 위한 rx_create_col_info를 추가합니다. <br/>`RxLocalParallel` 계산 컨텍스트를 사용하여 병렬 시나리오를 지원하기 위해 [rx_exec](/machine-learning-server/python-reference/revoscalepy/rx-exec)가 향상되었습니다.|
|**초기 릴리스** |  |  |
| | Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
| | R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
| | Python 서버    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

::: moniker-end

::: moniker range="=sql-server-2016"

<a name="bkmk_2016Installers"></a>

## <a name="sql-server-2016-cabs"></a>SQL Server 2016 CAB

SQL Server 2016 R Services의 경우 기본 릴리스는 RTM 버전 또는 서비스 팩 버전입니다.

|해제  |다운로드 링크  |
|---------|---------------|
|**SQL Server 2016 SP2 CU14-CU15**     |
|Microsoft R Open      |[SRO_3.5.2.777_1033.cab](https://go.microsoft.com/fwlink/?linkid=2134897)|
|Microsoft R 서버    |[SRS_9.4.7.958_1033.cab](https://go.microsoft.com/fwlink/?linkid=2136942)|
|**SQL Server 2016 SP2 CU6-CU13**     |
|Microsoft R Open     |[SRO_3.2.2.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079936&clcid=1033)|
|Microsoft R 서버    |[SRS_8.0.3.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079933&clcid=1033)|
|**SQL Server 2016 SP2 CU1-CU5**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R 서버    |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038)|
|**SQL Server 2016 SP2**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R 서버    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)|
|**SQL Server 2016 SP1 CU14**     |
|Microsoft R Open     |[SRO_3.2.2.16100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2080130&clcid=1033)|
|Microsoft R 서버    |[SRS_8.0.3.17200_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079935&clcid=1033)|
|**SQL Server 2016 SP1 CU1-CU13**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R 서버    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
|**SQL Server 2016 SP1**     |
|Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)|
|Microsoft R 서버     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)|
|**SQL Server 2016 CU4-CU9**     |
|Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
|Microsoft R 서버     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
|**SQL Server 2016 CU2-CU3**     |
|Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)|
|Microsoft R 서버     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)|
|**SQL Server 2016 CU1**     |
|Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)|
|Microsoft R 서버     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)|
|**SQL Server 2016 RTM**     |
|Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)|
|Microsoft R 서버     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)|

> [!NOTE]
> 
> SQL Server 2016 SP1 CU4 또는 SP1 CU5를 오프라인으로 설치할 때는 SRO_3.2.2.16000_1033.cab를 다운로드합니다. 설치 프로그램 대화 상자에 표시된 대로 FWLINK 831785에서 SRO_3.2.2.13000_1033.cab를 다운로드한 경우, 누적 업데이트를 설치하기 전에 파일 이름을 SRO_3.2.2.16000_1033.cab로 바꿉니다.

Microsoft R을 위한 소스 코드를 볼 수 있도록 .tar 형식의 아카이브로 다운로드가 제공됩니다. [R 서버 설치 프로그램 다운로드](/machine-learning-server/install/r-server-install-windows#download)

::: moniker-end

## <a name="next-steps"></a>다음 단계

[인터넷 액세스가 없는 컴퓨터에 누적 업데이트 적용](sql-ml-component-install-without-internet-access.md#apply-cu)

[인터넷 연결이 있는 컴퓨터에 누적 업데이트 적용](sql-ml-component-install-without-internet-access.md#apply-cu)

[독립형 서버에 누적 업데이트 적용](sql-machine-learning-standalone-windows-install.md#apply-cu)