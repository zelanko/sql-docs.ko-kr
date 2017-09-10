---
title: "기계 학습 인터넷 연결 되지 않은 구성 요소 설치 | Microsoft Docs"
ms.custom: 
ms.date: 04/20/2017
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
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7307104b9ad5df2bb8f034525cc82847d21a14bf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="installing-machine-learning-components-without-internet-access"></a>기계 학습 인터넷 연결 되지 않은 구성 요소를 설치 합니다.

R 및 Python 구성 요소는 SQL Server 2016 또는 SQL Server 2017와 함께 제공 되는 오픈 소스 이기 때문에 Microsoft는 기본적으로 Python 또는 R 구성 요소 설치 하지 않습니다.

대신, 관련 된 설치 관리자를 제공 하 고 패키지는 Microsoft 다운로드 센터 및 신뢰할 수 있는 다른 사이트에 편리한으로 제공 됩니다. 적절 한 라이선스에 동의 해야 한 다음 SQL Server 설치 프로그램은 설치 Python 또는 R 구성 요소에 있습니다.

이 항목에서는 설치 관리자와 오프 라인 설치 프로세스의 개요에 대 한 다운로드 위치를 제공 합니다.

## <a name="installation-process"></a>설치 프로세스

일반적으로 SQL Server 2016 및 SQL Server 2017에서 사용 되는 컴퓨터 구성 요소를 설치할 인터넷 연결이 필요 합니다. 컴퓨터 learnig 옵션 중 하나를 선택한 경우 SQL Server 설치 프로그램이 실행 될 때 설치를 확인 Python 또는 R 설치 관리자, 다른 모든 필수 구성 요소와 합니다. 인터넷에 연결 하는 경우 SQL Server를이 설치 합니다.

> [!IMPORTANT]
> 인터넷 연결 되지 않은 서버에서 설치를 계속 하기 전에 추가 설치 관리자를 다운로드 해야 합니다.

최소 버전은 지원 되거나 어셈블리를 설치 하는 SQL Server의 빌드 번호는 Python 또는 R 설치 관리자를 다운로드 해야 합니다.

서버의 구성에 따라.NET Core와 같은 추가 구성 요소를 할 수 있습니다.  참조 [추가 구성 요소](#bkmk_OtherComponents) 대 한 자세한 내용은 합니다.

설치 관리자를 다운로드 한 후 사용을 SQL Server 설치 프로그램의 일부로 기능을 설치 합니다.

### <a name="step-1-obtain-additional-installers"></a>1단계. 가져올 추가 설치 관리자

에 대 한 **R** SQL Server 2016 및 SQL Server 2017에서 두 명의 서로 다른 설치 관리자를 가져오려는 필요 합니다. SQL Server 설치 마법사는 설치 관리자가 올바른 순서로 설치되도록 합니다.

+ 설치 프로그램의 **SRO** 이름에는 오픈 소스 구성 요소를 제공 합니다.
+ 와 Insallers **SRS** 이름에 데이터베이스 통합에 대 한 포함 하 여 Microsoft에서 제공 하는 구성 요소를 포함 합니다.


에 대 한 **Python** SQL Server 2017 년에 단일 CAB 파일 및 모든 필수 구성 요소를 다운로드 합니다.


1. 인터넷 액세스를 통해 [Microsoft 다운로드 센터 사이트](#installerlocs)에서 컴퓨터로 설치 관리자를 다운로드하여 실행하는 대신 저장합니다.
2. 컴퓨터 학습 구성 요소를 설치할 컴퓨터에 설치 관리자 (CAB) 파일을 복사 합니다.
3. 현재 설치 마법사는 기본적으로 영어를 설치합니다. 다른 언어를 사용 하 여를 설치 하려면 설치 관리자 파일 이름을 여기에서 설명한 대로 수정: [다른 언어 로캘을에 필요한 수정](#modslocales)합니다.
4. MPI 또는.NET Core과 같이 필요한 모든 추가 구성 요소를 다운로드 합니다.
5. 필요에 따라 오픈 소스 구성 요소에 대 한 보관 된 소스 코드를 다운로드할 수 있지만 SQL Server 설치 프로그램에 필요 하지 않습니다이 이며 언제 든 지 종료할 수 있습니다. 자세한 내용은 참조 [Windows 용 R 서버](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)합니다.


> [!NOTE]
> 설치할 SQL Server 버전과 일치하는 파일을 다운로드해야 합니다.
> 
> Python에 대 한 지원이 SQL Server 2017 CTP 2.0에서 제공 됩니다. SQL Server 2016 이전 버전에서는 Python 지원 하지 않습니다.

SQL Server 2016에서 R Services에 대 한 오프 라인 설치 프로세스의 단계별 연습에서는 문서, 권장는 [SQL Server 고객 자문 팀](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)합니다. 이 문서에서는 패치 및 통합 설치 시나리오를 다룹니다.


### <a name="step-2-run-offline-setup-using-the-sql-server-setup-wizard"></a>2단계. SQL Server 설치 마법사를 사용 하 여 오프 라인 설치를 실행 합니다.

1. SQL Server 설치 마법사를 실행합니다.
2. 설치 마법사 라이선스 페이지가 표시 되 면 클릭 **Accept**합니다.
3. 에 대 한 묻는 대화 상자가 열립니다는 **설치 경로** 필요한 패키지 합니다.
4. 클릭 **찾아보기** 앞에서 복사한 설치 관리자 파일을 포함 하 여 폴더를 찾습니다.
5. 올바른 파일을 찾으면 **다음**을 클릭하여 구성 요소가 사용 가능함을 표시합니다.
10. SQL Server 설치 마법사를 완료합니다.
11. 서비스가 활성화 되어 있는지 확인 하는 데 필요한 설치 후 단계를 수행 합니다.

## <a name="installerlocs"></a>다운로드

릴리스  |다운로드 링크  
---------|---------
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
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)  |
**SQL Server 2016 SP 1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 SP 1 GDR**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**SQL Server 2017 CTP 1**     |
Microsoft R Open     |[SRO_3.3.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_9.0.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**SQL Server 2017 CTP 1.1** |
Microsoft R Open     |[SRO_3.3.2.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834568)
Microsoft R Server     |[SRS_9.0.1.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834567)
**SQL Server 2017 CTP 1.4** |
Microsoft R Open     |[SRO_xxxx_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842483)
Microsoft R Server     |[SRS_xxx.xxx_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842482)
**SQL Server 2017 CTP 2.0** |
Microsoft R Open     |[SRO_3.3.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842800)
Microsoft R Server     |[SRS_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842799)
Microsoft Python 열기     |[SPO_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842828)
Microsoft Python 서버    |[SPS_9.1.0.0__1033.cab](https://go.microsoft.com/fwlink/?LinkId=842848)

Microsoft R에 대 한 소스 코드를 보고 하려는 경우 다운로드할 수 있는.tar 형식으로 보관으로: [다운로드 R 서버 설치 관리자](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#download)

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

인터넷에 연결된 컴퓨터에서 SQL Server 설치의 일부로 .cab 파일을 다운로드하는 경우 설치 마법사에서 로컬 언어를 검색하고 설치 관리자의 언어를 자동으로 변경합니다.

그러나 인터넷에 연결되지 않은 컴퓨터에 지역화된 버전의 SQL Server 중 하나를 설치 중이며 R 설치 관리자를 로컬 공유로 다운로드하는 경우에는 다운로드한 파일의 이름을 수동으로 편집하고 설치 중인 언어에 맞는 올바른 언어 식별자를 삽입해야 합니다.

예를 들어 일본어 버전의 SQL Server를 설치하는 경우 파일 이름을 SRS_8.0.3.0_**1033**.cab에서 SRS_8.0.3.0_**1041**.cab로 변경합니다.


## <a name="slipstream-upgrades"></a>통합 설치 업그레이드

통합 설치는 실패한 인스턴스 설치에 패치나 업데이트를 적용하여 기존 문제를 해결하는 기능을 말합니다. 이 방법은 설치를 수행할 때 동시에 SQL Server가 업데이트되므로 이후에 별도로 다시 시작할 필요가 없는 장점이 있습니다.

+ 서버가 인터넷에 연결되어 있지 않으면 SQL Server 설치 관리자를 다운로드하고 나서 업데이트 프로세스를 시작하기 **전에** R 구성 요소 설치 관리자의 일치하는 버전을 다운로드해야 합니다.  R 구성 요소는 SQL Server와 함께 기본적으로 포함 되지 않습니다.

+ 있다면 *추가* 에 이러한 구성 요소는 *기존* 설치를 업데이트 된 버전의 SQL Server 설치 관리자를 사용 하 고 해당 버전의 추가 구성 요소를 업데이트 합니다. R 기능이 설치 되도록 상태임을 지정 하면 설치 프로그램은 기계 학습 구성 요소에 대 한 설치 관리자의 일치 하는 버전 검색 합니다.

## <a name="command-line-arguments-for-setup"></a>설치를 위한 명령줄 인수

무인된 설치를 수행할 때는 다음 명령줄 인수를 제공 해야 합니다. 필수 구성 요소를 참고 추가 설치 하려면 모든 추가 플래그를 설정할 필요가 없습니다. .NET core 같은 필수 구성 요소는 기본적으로 자동으로 설치 됩니다.

**설치 관리자의 위치**

- `/UPDATESOURCE`SQL Server 업데이트 설치 관리자를 포함 하는 로컬 파일의 위치를 지정 하려면
- `/MRCACHEDIRECTORY`R 구성 요소 CAB 파일을 포함 하는 폴더를 지정 하려면

**SQL Server 2016의 R 구성 요소**

- `/ADVANCEDANALYTICS`외부 스크립트에 대 한 엔진 지원
- `/IACCEPTROPENLICENSETERMS="True"`별도 R 사용권 계약을 적용 하려면

**SQL Server SQL Server 2017에 R 구성 요소**

- `/ADVANCEDANALYTICS`외부 스크립트에 대 한 엔진 지원
- `/SQL_INST_MR`R을 사용 하려면
- `/IACCEPTROPENLICENSETERMS="True"`별도 R 사용권 계약을 적용 하려면

**SQL Server 2017에 Python 구성 요소**

- `/ADVANCEDANALYTICS`외부 스크립트에 대 한 엔진 지원
- `/SQL_INST_MPY`Python을 사용 하려면
- `/IACCEPTPYTHONLICENSETERMS="True"`별도 R 사용권 계약을 적용 하려면

> [!TIP]
> R 서비스 지원 팀에서이 문서에서는 SQL Server 2016의 무인된 설치 또는 R services의 업그레이드를 수행 하는 방법을 보여 줍니다: [인터넷 액세스가 없는 컴퓨터에 R 서비스 배포](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)합니다.

## <a name="see-also"></a>관련 항목:

[Microsoft R Server 설치](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)


