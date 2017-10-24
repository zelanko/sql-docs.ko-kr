---
title: "인터넷 연결 되지 않은 컴퓨터 학습 구성 요소 설치 | Microsoft Docs"
ms.custom: 
ms.date: 10/0522/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 30
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: f2b67ff49d5773890ff94f44eddeb01f2d5aaddf
ms.contentlocale: ko-kr
ms.lasthandoff: 10/06/2017

---
# <a name="installing-machine-learning-components-without-internet-access"></a>인터넷 연결 되지 않은 컴퓨터 학습 구성 요소 설치

R 및 Python 구성 요소는 SQL Server 2016 및 SQL Server 2017와 함께 제공 되는 오픈 소스 이기 때문에 Microsoft는 기본적으로 Python 또는 R 구성 요소 설치 하지 않습니다.

대신, 관련 된 설치 관리자를 제공 하 고 패키지는 Microsoft 다운로드 센터 및 신뢰할 수 있는 다른 사이트에 편리한으로 제공 됩니다. 적절 한 라이선스에 동의 해야 하 고 SQL Server 설치 프로그램 사용자에 대 한 Python 또는 R 구성 요소를 설치 하는 합니다.

이 항목에서는 설치 관리자와 오프 라인 설치 프로세스의 개요에 대 한 다운로드 위치를 제공 합니다.

## <a name="installation-process"></a>설치 프로세스

일반적으로 SQL Server 2016 및 SQL Server 2017에서 사용 되는 컴퓨터 구성 요소를 설치할 인터넷 연결이 필요 합니다. 기계 학습 옵션 중 하나를 선택한 경우 SQL Server 설치 프로그램 실행, 설치 확인 Python 또는 R에 대 한 설치 관리자, 다른 모든 필수 구성 요소와 합니다.

+ **컴퓨터에 있는 경우 인터넷에 연결**

    SQL Server, 구성 요소를 다운로드 힙이고 설치 하는 동안 설치를 찾습니다. 오픈 소스는 각 구성 요소 (R 또는 Python) 설치에 대해 별도로 사용 조건에 동의 해야 합니다.

+ **컴퓨터에 인터넷 액세스가 없는 경우**

    설치를 계속 하기 전에 추가 설치 관리자를 다운로드 해야 합니다. 최소한를 설치 하는 SQL Server의 버전에 지원 되는 R, Python 설치 관리자를 다운로드 합니다.

    서버의 구성에 따라 추가 구성 요소를 할 수 있습니다.  참조 [추가 구성 요소](#bkmk_OtherComponents) 대 한 자세한 내용은 합니다.

    설치 관리자를 다운로드 한 후 사용을 SQL Server 설치 프로그램의 일부로 기능을 설치 합니다.

### <a name="step-1-obtain-additional-installers"></a>1단계. 가져올 추가 설치 관리자

에 대 한 **R** SQL Server 2016 및 SQL Server 2017에서 두 명의 서로 다른 설치 관리자를 가져오려는 필요 합니다. SQL Server 설치 마법사가 올바른 순서 대로 설치 되어 있는지 확인 합니다.

+ 설치 프로그램의 **SRO** 이름에는 오픈 소스 구성 요소를 제공 합니다.
+ 설치 프로그램의 **SRS** 이름에 데이터베이스 통합에 대 한 포함 하 여 Microsoft에서 제공 하는 구성 요소를 포함 합니다.

에 대 한 **Python** SQL Server 2017 년에 단일 CAB 파일 및 모든 필수 구성 요소를 다운로드 합니다.

1. 설치 관리자 다운로드는 [Microsoft 다운로드 센터 사이트](#installerlocs) 실행 하지 않고 설치 프로그램을 저장 하 고 인터넷에 연결 된 컴퓨터에 있습니다.
2. 시스템 학습 구성 요소를 설치 하려는 컴퓨터에 설치 관리자 (CAB) 파일을 복사 합니다.
3. SQL Server 2016 설치 마법사는 기본적으로 영어를 설치 합니다. 다른 언어를 사용 하 여 설치 하려면 설치 관리자 파일 이름의 수정 여기에서 설명한 대로 필요한: [다양 한 언어 로캘에 대 한 수정이 필요한](#modslocales)합니다.
    SQL Server 2017 년에 대 한 올바른 언어 인스턴스 로캘을 기반으로 식별 됩니다.
4. MPI 또는.NET Core과 같이 필요한 모든 추가 구성 요소를 다운로드 합니다.
5. 필요에 따라 오픈 소스 구성 요소에 대 한 보관 된 소스 코드를 다운로드할 수 있지만 SQL Server 설치 프로그램에 필요 하지 않습니다이 이며 언제 든 지 종료할 수 있습니다. 자세한 내용은 참조 [Windows 용 R 서버](https://docs.microsoft.com/r-server/install/r-server-install-windows)합니다.

SQL Server 2016에서 R Services에 대 한 오프 라인 설치 프로세스의 단계별 연습에서는 문서, 권장는 [SQL Server 고객 자문 팀](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)합니다. 문서 스크린샷을 포함 하 고 패치 및 통합 설치 시나리오에 대해서도 설명 합니다.

### <a name="step-2-run-offline-setup-using-the-sql-server-setup-wizard"></a>2단계. SQL Server 설치 마법사를 사용 하 여 오프 라인 설치를 실행 합니다.

1. SQL Server 설치 마법사를 실행합니다.
2. 설치 마법사 라이선스 페이지가 표시 되 면 클릭 **Accept**합니다.
3. 에 대 한 묻는 대화 상자가 열립니다는 **설치 경로** 필요한 패키지 합니다.
4. 클릭 **찾아보기** 앞에서 복사한 설치 관리자 파일을 포함 하 여 폴더를 찾습니다.
5. 올바른 파일을 찾으면 **다음**을 클릭하여 구성 요소가 사용 가능함을 표시합니다.
10. SQL Server 설치 마법사를 완료합니다.
11. 서비스가 활성화 되어 있는지 확인 하는 데 필요한 설치 후 단계를 수행 합니다.

## <a name="installerlocs"></a>컴퓨터 학습 구성 요소를 다운로드 하는 위치

> [!NOTE]
> 설치 하는 SQL Server의 버전과 일치 하는 파일을 가져올 해야 합니다.
> 
> SQL Server 2017 CTP 2.0 부터는 Python에 대 한 지원이 제공 됩니다. SQL Server 2016 이전 버전에서는 Python 지원 하지 않습니다.

+ [SQL Server 2016에 대 한 R 구성 요소를 가져오려는](#bkmk_2016Installers)

+ [SQL Server 2017에 대 한 Python 또는 R 구성 요소를 가져오려는](#bkmk_2017Installers)

### <a name="bkmk_2017Installers"></a>SQL Server 2017에 대 한 다운로드

릴리스  |다운로드 링크  |
---------|---------|
**SQL Server 2017 CTP 1**     |
Microsoft R Open     |[SRO_3.3.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_9.0.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**SQL Server 2017 CTP 1.1** |
Microsoft R Open     |[SRO_3.3.2.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834568)
Microsoft R Server     |[SRS_9.0.1.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834567)
**SQL Server 2017 CTP 1.4** |
Microsoft R Open     |[SRO_3.3.2.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842483)
Microsoft R Server     |[SRS_9.0.2.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842482)
**SQL Server 2017 CTP 2.0** |
Microsoft R Open     |[SRO_3.3.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842800)
Microsoft R Server     |[SRS_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842799)
Microsoft Python 열기     |[SPO_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842828)
Microsoft Python 서버    |[SPS_9.1.0.0__1033.cab](https://go.microsoft.com/fwlink/?LinkId=842848)
**SQL Server 2017 RC1** |
Microsoft R Open     |[SRO_3.3.3.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851503)|
Microsoft R Server     |[SRS_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851498)|
Microsoft Python 열기     |[SPO_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851499)|
Microsoft Python 서버    |[SPS_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851504)|
**SQL Server 2017 RC 2** |
Microsoft R Open     |[SRO_3.3.3.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851493)|
Microsoft R Server     |[SRS_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851505)|
Microsoft Python 열기     |[SPO_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851506)|
Microsoft Python 서버    |[SPS_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851497)|
**SQL Server 2017 RTM** |
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python 열기     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python 서버    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |
**SQL Server 2017 CU1** |
Microsoft R Open     |prervious 사용|
Microsoft R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
Microsoft Python 열기     |이전에 사용 하 여 |
Microsoft Python 서버    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) |

### <a name="bkmk_2016Installers"></a>SQL Server 2016에 대 한 다운로드

> [!IMPORTANT]
> 
> SQL Server 2016 SP1 CU4 또는 CU5 s p 1을 오프 라인으로 설치할 때 SRO_3.2.2.16000_1033.cab 다운로드 합니다. 에서 다운로드 한 SRO_3.2.2.13000_1033.cab FWLINK 831785 설정 대화 상자에 표시 된 대로, 하는 경우 누적 업데이트를 설치 하기 전에 파일을 SRO_3.2.2.16000_1033.cab로 바꿉니다.

릴리스  |다운로드 링크  |
---------|---------|
**SQL Server 2016 RTM**     |
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)
**SQL Server 2016 CU 1**     |
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)
**SQL Server 2016 CU 2**     |
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)
**SQL Server 2016 CU 3**     |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server     | 변경 없음 이전에 사용 하 여 |
**SQL Server 2016 CU 4**     |
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
**SQL Server 2016 CU 5**     |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server     |변경 없음 이전에 사용 하 여|
**SQL Server 2016 CU 6**     |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server     |[SRS_8.0.3.14000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850316)  |
**SQL Server 2016 CU 7**     |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server     |변경 없음 이전에 사용 하 여 |
**SQL Server 2016 SP 1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 SP 1 c u 1**     |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server     |변경 없음 이전에 사용 하 여|
**SQL Server 2016 SP 1 c u 2**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
**SQL Server 2016 SP 1 CU3**     |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server     |변경 없음 이전에 사용 하 여|
**SQL Server 2016 SP 1 CU4 및 GDR**     |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)
**SQL Server 2016 SP 1 CU5**     |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server    |변경 없음 이전에 사용 하 여 |

Microsoft R에 대 한 소스 코드를 보고 하려는 경우 다운로드할 수 있는.tar 형식으로 보관으로: [다운로드 R 서버 설치 관리자](https://docs.microsoft.com/r-server/install/r-server-install-windows#download)

### <a name = "bkmk_OtherComponents"></a>추가 필수 구성 요소

사용자 환경에 따라 다음 필수 구성 요소에 대한 설치 관리자의 로컬 복사본을 만들어야 할 수 있습니다.

구성 요소  |버전
---------|---------
[SQL Server 2016용 Microsoft AS OLE DB 공급자](https://go.microsoft.com/fwlink/?linkid=834405)     |  13.0.1601.5
[Microsoft .NET Core](https://go.microsoft.com/fwlink/?linkid=834319)     | 1.0.1
[Microsoft MPI](https://go.microsoft.com/fwlink/?linkid=834316)     | 7.1.12437.25
[Microsoft Visual C++ 2013 재배포 가능](https://go.microsoft.com/fwlink/?linkid=799853)     | 12.0.30501.0
[Microsoft Visual C++ 2015 재배포 가능](https://go.microsoft.com/fwlink/?linkid=828641)     | 14.0.23026.0


## <a name="modslocales"></a>다른 언어 로캘에 대 한 설치

다운로드 하는 경우는 합니다. 설치 마법사에 인터넷 연결 된 컴퓨터에서 SQL Server 설치 프로그램의 일부로 CAB 파일이 로컬 언어를 감지 하 고 자동으로 설치 관리자의 언어를 변경 합니다.

그러나 SQL Server의 버전을 따라 인터넷 연결 되지 않은 컴퓨터에 지역화 된 R 구성 요소를 설치 하려면 추가 단계를 수행 해야 할 수 있습니다.

+ **SQL Server 2016에 대 한**

   로컬 공유로 R 설치 관리자를 다운로드 한 후에 수동으로 설치 하는 언어에 대 한 올바른 언어 식별자를 삽입 하는 다운로드 한 파일의 이름을 편집 해야 합니다.

    예를 들어 일본어 버전의 SQL Server를 설치 하는 파일의 이름에서에서 변경한 SRS_8.0.3.0_**1033**SRS_8.0.3.0_에.cab**1041**.cab 합니다.

    > [!IMPORTANT]
    > 이 문제는만 초기 버전을 적용 하 고 이후 릴리스에서 수정 되었습니다.
    > 설치 관리자의 언어를 설치할 수 없습니다는 메시지를 반환 하는 경우에이 해결 방법을 사용 합니다.

+ **SQL server 2017**

    다운로드는 합니다. Python 또는 R 구성 요소에 대 한 CAB 파일입니다.
    
    언어 서버 언어로 검색 됩니다. 올바른 로캘로 다운로드 한를 사용 하 여 자동으로 설치 됩니다. CAB 파일입니다.

## <a name="slipstream-upgrades"></a>통합 설치 업그레이드

통합 설치는 실패한 인스턴스 설치에 패치나 업데이트를 적용하여 기존 문제를 해결하는 기능을 말합니다. 이 방법은 설치를 수행할 때 동시에 SQL Server가 업데이트되므로 이후에 별도로 다시 시작할 필요가 없는 장점이 있습니다.

+ 서버가 인터넷에 연결되어 있지 않으면 SQL Server 설치 관리자를 다운로드하고 나서 업데이트 프로세스를 시작하기 **전에** R 구성 요소 설치 관리자의 일치하는 버전을 다운로드해야 합니다.  R 구성 요소는 SQL Server와 함께 기본적으로 포함 되지 않습니다.

+ 있다면 *추가* 에 이러한 구성 요소는 *기존* 설치를 업데이트 된 버전의 SQL Server 설치 관리자를 사용 하 고 해당 버전의 추가 구성 요소를 업데이트 합니다. R 기능이 설치 되도록 상태임을 지정 하면 설치 관리자 구성 요소를 학습 하는 컴퓨터에 대 한 설치 관리자의 일치 하는 버전을 찾습니다.

## <a name="command-line-arguments-for-setup"></a>설치를 위한 명령줄 인수

무인된 설치를 수행할 때는 다음 명령줄 인수를 제공 해야 합니다. 그러나 필요가 없습니다 추가 필수 구성 요소; 설치 된 추가 플래그를 설정 하려면 .NET core 같은 필수 구성 요소는 기본적으로 자동으로 설치 됩니다.

**설치 관리자의 위치**

- `/UPDATESOURCE`SQL Server 업데이트 설치 관리자를 포함 하는 로컬 파일의 위치를 지정 하려면
- `/MRCACHEDIRECTORY`R 구성 요소 CAB 파일을 포함 하는 폴더를 지정 하려면

**SQL Server 2016의 R 구성 요소**

- `/ADVANCEDANALYTICS`외부 스크립트에 대 한 엔진 지원
- `/IACCEPTROPENLICENSETERMS="True"`별도 R 사용권 계약을 적용 하려면

**SQL Server 2017에 R 구성 요소**

- `/ADVANCEDANALYTICS`외부 스크립트에 대 한 엔진 지원
- `/SQL_INST_MR`R을 사용 하려면
- `/IACCEPTROPENLICENSETERMS="True"`별도 R 사용권 계약을 적용 하려면

**SQL Server 2017에 Python 구성 요소**

- `/ADVANCEDANALYTICS`외부 스크립트에 대 한 엔진 지원
- `/SQL_INST_MPY`Python을 사용 하려면
- `/IACCEPTPYTHONLICENSETERMS="True"`별도 R 사용권 계약을 적용 하려면


> [!NOTE]
> SQL Server 설치 프로그램에서 매개 변수를 사용 하 여 실행 패드에 대 한 서비스 계정을 변경할 수 없습니다. 기본 서비스 계정을 사용 하 여 설치 하 고 다음 SQL Server 구성 관리자를 사용 하 여 서비스 계정을 수정 하는 것이 좋습니다. 이렇게 하면 실행 패드 서비스를 다시 시작 해야 합니다.

## <a name="see-also"></a>참고 항목

[Microsoft R Server 설치](https://docs.microsoft.com/r-server/install/r-server-install-windows)

R 서비스 지원 팀에서이 문서에서는 SQL Server 2016의 무인된 설치 또는 R services의 업그레이드를 수행 하는 방법을 보여 줍니다: [인터넷 액세스가 없는 컴퓨터에 R 서비스 배포](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)합니다.

