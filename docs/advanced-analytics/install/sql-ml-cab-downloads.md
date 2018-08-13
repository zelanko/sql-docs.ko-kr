---
title: SQL Server 누적 업데이트에 대 한 CAB 다운로드 | Microsoft 문서
description: SQL Server 2017의 Machine Learning Services 및 SQL Server 2016 R Services에 대 한 CAB 다운로드 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/02/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6a2893e976e64315a1aad742062e962269439b72
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39566324"
---
# <a name="cab-downloads-for-cumulative-updates-of-sql-server-in-database-analytics-instances"></a>인스턴스가 SQL Server 데이터베이스 내 분석의 누적 업데이트에 대 한 CAB 다운로드

SQL Server 인스턴스에 데이터베이스 내 분석에 대해 구성 된 CAB 파일을 설치 하 고 서비스를 통해 SQL Server 설치 프로그램에서 제공 되는 R 및 Python 기능을 포함 합니다. 

인터넷에 연결 하는 서버에서 CAB 업데이트는 Windows Update를 통해 일반적으로 적용 됩니다. 연결이 끊어진된 서버를 수동으로 업데이트 해야 합니다. 이 문서에서는 인터넷에서 연결이 끊어진 서버를 수동으로 업데이트할 수 있도록 SQL Server 2017 Machine Learning Services (R 및 Python) 또는 SQL Server 2016 R Services의 각 누적 업데이트에 대 한 CAB 파일 다운로드 링크를 제공 합니다. 

## <a name="prerequisites"></a>사전 요구 사항

초기 설치를 시작 합니다.

+ SQL Server 2017 Machine Learning Services의 초기 릴리스는 초기 설치는 합니다. 

+ SQL Server 2016 R Services의 초기 릴리스, SP1 또는 SP2를 사용 하 여 시작할 수 있습니다. 

자세한 내용은 [인터넷에 액세스 하지 않고 구성 요소를 학습 하는 SQL Server 설치 컴퓨터](sql-ml-component-install-without-internet-access.md)합니다.

초기 설치를 수행한 후 수행할 수 있습니다는 [업그레이드를 통합 설치할](sql-ml-component-install-without-internet-access.md#slipstream-upgrades) 업데이트 된 machine learning 기능을 사용 하 여 CAB 파일을 포함 하는 합니다.

CAB 파일은 역방향 시간 순서로 나열 됩니다. CAB 파일을 다운로드 하 고 대상 컴퓨터에 전송할 때 편리한 폴더 같은 배치할 **다운로드** 또는 설치 사용자의 %temp% 폴더입니다.

## <a name="sql-server-2017-cabs"></a>SQL Server 2017 cab 파일

릴리스  |다운로드 링크  |
---------|---------|
**SQL Server 2017 CU8-cu9까지 포함** |
Microsoft R Open     |변경 없음 사용 하 여 이전 [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
Microsoft R Server      |[SRS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874708&clcid=1033)|
Microsoft Python 열기     |변경 없음 사용 하 여 이전 [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)|
Microsoft Python 서버    |[SPS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874707&clcid=1033)]|
**SQL Server 2017 CU6-CU7** |
Microsoft R Open     |변경 없음 사용 하 여 이전 [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
Microsoft R Server      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
Microsoft Python 열기     |변경 없음 사용 하 여 이전 [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)|
Microsoft Python 서버    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)|
**SQL Server 2017 CU5** |
Microsoft R Open     |변경 없음 사용 하 여 이전 [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
Microsoft R Server      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)|
Microsoft Python 열기     |변경 없음 사용 하 여 이전 [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)|
Microsoft Python 서버    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)|
**SQL Server 2017 CU4** |
Microsoft R Open     |변경 없음 사용 하 여 이전 [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
Microsoft R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
Microsoft Python 열기     |변경 없음 사용 하 여 이전 [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)|
Microsoft Python 서버    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
**SQL Server 2017 CU3** |
Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
Microsoft R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
Microsoft Python 열기     |변경 없음 사용 하 여 이전 [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)|
Microsoft Python 서버    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)|
**SQL Server 2017 CU1에서 CU2** |
Microsoft R Open     |변경 없음 사용 하 여 이전 [SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
Microsoft Python 열기     |변경 없음 사용 하 여 이전 [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)|
Microsoft Python 서버    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) |
**SQL Server 2017 초기 릴리스** |
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python 열기     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python 서버    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |


<a name="bkmk_2016Installers"></a>

## <a name="sql-server-2016-cabs"></a>SQL Server 2016 cab 파일

SQL Server 2016 R Services에 대 한 초기 릴리스는 RTM 버전 또는 서비스 팩 버전입니다.

릴리스  |다운로드 링크  |
---------|---------------|
**SQL Server 2016 SP2 CU1에서 CU2**     |
Microsoft R Open     |[SRO_3.2.2.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039)|
Microsoft R Server    |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038)|
**SQL Server 2016 SP1 CU4 CU10**     |
Microsoft R Open     |변경 없음 사용 하 여 이전 [SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)
**SQL Server 2016 SP1 CU1에서 CU3**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
**SQL Server 2016 SP1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)=
**SQL Server 2016 CU4-cu9까지 포함**     |
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
**SQL Server 2016 CU2 CU3**     |
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)
**SQL Server 2016 CU1**     |
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)
**SQL Server 2016 RTM**     |
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)

> [!NOTE]
> 
> SQL Server 2016 SP1 CU4 또는 SP1 CU5 오프 라인으로 설치 하는 경우 SRO_3.2.2.16000_1033.cab를 다운로드 합니다. 설치 대화 상자에 표시 된 대로 SRO_3.2.2.13000_1033.cab FWLINK 831785에서 다운로드 한 경우 누적 업데이트를 설치 하기 전에 파일을 SRO_3.2.2.16000_1033.cab로 바꿉니다.

Microsoft R에 대 한 소스 코드를 보고 하려는 경우 다운로드할 수 있습니다.tar 형태로 아카이브로: [R Server 다운로드 설치 관리자](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

# <a name="see-also"></a>참고자료

[SQL Server 기계 학습 인터넷 액세스 없이 구성 요소를 설치 합니다.](sql-ml-component-install-without-internet-access.md)
