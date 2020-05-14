---
title: Linux 및 macOS 기반 ODBC Driver for SQL Server 릴리스 정보
description: Microsoft ODBC Driver for SQL Server의 릴리스 버전에서 새롭게 제공되는 기능과 변경된 기능에 대해 알아봅니다.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: v-jizho2
ms.technology: connectivity
ms.topic: conceptual
author: v-chojas
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: c2fe32e1a86273d071801fed9d2ffb8806d54ce6
ms.sourcegitcommit: 37a3e2c022c578fc3a54ebee66d9957ff7476922
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922206"
---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Linux 및 macOS 기반 Microsoft ODBC Driver for SQL Server에 대한 릴리스 정보

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 문서에서는 Linux 및 macOS 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC 드라이버의 각 버전 릴리스의 새로운 기능을 나열하고 설명합니다.

<!--
Going forward, please use the new 2-column markdown table for each new H2 version section.
And we are keeping the H2 titles much shorter, partly by removing redundant or obvious info.
We want to track the Month YYYY each new version H2 section is added, at the end of the H2 title.
This is the new standard format for Release Notes article content.

OLD     FILE NAME:    linux-mac/release-notes.md
NOW NEW FILE NAME:    linux-mac/release-notes-odbc-sql-server-linux-mac.md

Thank you.
GeneMi.  2019/04/03.
-->

## <a name="17522-april-2020-alpine-linux-only"></a>17.5.2.2, 2020년 4월(Alpine Linux만 해당)

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| 버그가 수정 되었습니다. | [버그 수정](../bug-fixes.md)을 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="1752-march-2020"></a>17.5.2, 2020년 3월

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| 관리 ID로 Azure Key Vault 인증 지원 | [Always Encrypted와 ODBC 드라이버 사용](../using-always-encrypted-with-the-odbc-driver.md)을 참조하세요. |
| 추가 Azure Key Vault 엔드포인트 지원 | [Always Encrypted와 ODBC 드라이버 사용](../using-always-encrypted-with-the-odbc-driver.md)을 참조하세요. |
| 버그 수정. | [버그 수정](../bug-fixes.md)을 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="175-january-2020"></a>17.5, 2020년 1월

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| 서버를 왕복하지 않고 SPID를 검색하는 SQL_COPT_SS_SPID 연결 특성 | [DSN 및 연결 문자열 특성과 키워드](../dsn-connection-string-attribute.md)를 참조하세요. |
| Debian 및 Ubuntu에서 `debconf`를 통해 EULA 승인 표시를 지원 | [드라이버 설치](./installing-the-microsoft-odbc-driver-for-sql-server.md)를 참조하세요. |
| 지원되는 새 배포. | &bull; &nbsp; &nbsp; Alpine Linux(3.10, 3.11)<br/>&bull; &nbsp; &nbsp; Oracle Linux 8<br/>&bull; &nbsp; &nbsp; Ubuntu 19.10<br/>&bull; &nbsp; &nbsp; macOS 10.15 |
| 버그 수정. | [버그 수정](../bug-fixes.md)을 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="1742-october-2019"></a>17.4.2, 2019년 10월

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| 추가 Azure Key Vault 엔드포인트 지원 | [Always Encrypted와 ODBC 드라이버 사용](../using-always-encrypted-with-the-odbc-driver.md)을 참조하세요. |
| 데이터 분류 버전 설정 지원 | [데이터 분류](../data-classification.md#bkmk-version)를 참조하세요. |
| 버그 수정. | [버그 수정](../bug-fixes.md)을 참조하세요. |
| &nbsp; | &nbsp; |

**알려진 문제:**

보안 enclave 및 Azure Key Vault에서 Always Encrypted를 사용하는 경우 홀수 키 경로 길이는 CMK 서명 확인 오류가 발생할 수 있습니다. 이 문제가 발생하는 경우 AKV 키의 이름을 바꿔 키 경로의 길이를 한 문자씩 변경해 보세요.

## <a name="174-august-2019"></a>17.4, 2019년 8월

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| 보안 Enclave를 사용한 Always Encrypted. | [Always Encrypted와 ODBC 드라이버 사용](../using-always-encrypted-with-the-odbc-driver.md)을 참조하세요. |
| OpenSSL의 동적 로드 | [프로그래밍 지침](programming-guidelines.md#bkmk-openssl)을 참조하세요. |
| 구성 가능한 TCP 연결 유지 설정입니다. | [SQL Server에 연결](connection-string-keywords-and-data-source-names-dsns.md)을 참조하세요. |
| 버그 수정. | [버그 수정](../bug-fixes.md)을 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="173-february-2019"></a>17.3, 2019년 2월

| 새 항목 | 세부 정보 |
| :------- | :------ |
| 지원되는 새 배포. | &bull; &nbsp; &nbsp; SUSE 15<br/>&bull; &nbsp; &nbsp; Ubuntu 18.10<br/>&bull; &nbsp; &nbsp; macOS 10.14 |
| Azure Active Directory 관리 서비스 ID(시스템 및 사용자 할당) 인증 모드. | [ODBC 드라이버에서 Azure Active Directory 사용](../using-azure-active-directory.md)을 참조하세요. |
| Always Encrypted 열에 대해 입력 매개 변수를 스트리밍할 수 있음. | 자세한 내용은 [Always Encrypted를 사용할 때 ODBC 드라이버의 제한 사항](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted)을 참조하세요. |
| XA 분산 트랜잭션. | [XA 트랜잭션 사용](../use-xa-with-dtc.md)을 참조하세요.<br/><br/>XA는 둘 이상의 서버 쪽 데이터 스토리지 시스템에 액세스하는 전역 트랜잭션을 실행하기 위한 표준인 _확장 아키텍처_에 대한 두문자어입니다. |
| &nbsp; | &nbsp; |

## <a name="172-july-2018"></a>17.2, 2018년 7월

| 새 항목 | 세부 정보 |
| :------- | :------ |
| 지원되는 새 배포. | &bull; &nbsp; &nbsp; Ubuntu 18.04 |
| Azure SQL Database 및 SQL Server에 대한 데이터 분류. | [데이터 분류](../data-classification.md)를 참조하세요. |
| UTF-8 서버 인코딩 지원. | &nbsp; |
| `SQLBrowseConnect` | &nbsp; |
| `libcurl`에 대한 동적 종속성. | 이 버전부터 `libcurl` 패키지는 명시적 종속성이 아닙니다.<br/>Azure Key Vault 또는 Azure Active Directory 인증을 사용하는 경우 OpenSSL 또는 NSS용 `libcurl` 패키지가 필요합니다.<br/>`libcurl`에 관한 오류가 발생하는 경우 해당 패키지가 설치되었는지 확인하십시오. |
| 연결 문자열에 ConnectRetryCount 및 ConnectRetryInterval 키워드를 포함하는 유휴 연결 복원력. | &bull; &nbsp; &nbsp; 연결 재시도 횟수를 검색하려면 `SQL_COPT_SS_CONNECT_RETRY_COUNT`(읽기 전용)를 사용합니다.<br/><br/>&bull; &nbsp; &nbsp; 연결 재시도 간격의 길이를 검색하려면 `SQL_COPT_SS_CONNECT_RETRY_INTERVAL`(읽기 전용)을 사용합니다.<br/><br/>[Windows ODBC 드라이버의 연결 복원력](../windows/connection-resiliency-in-the-windows-odbc-driver.md)을 참조하세요. |
| 버그 수정. | [버그 수정](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="171-march-2018"></a>17.1, 2018년 3월

| 새 항목 | 세부 정보 |
| :------- | :------ |
| `SQL_COPT_SS_CEKCACHETTL` 및 `SQL_COPT_SS_TRUSTEDCMKPATHS` 연결 특성 지원. | &bull; &nbsp; &nbsp; `SQL_COPT_SS_CEKCACHETTL`을 사용하여 열 암호화 키의 로컬 캐시가 존재하는 시간을 제어할 뿐만 아니라 플러시할 수도 있습니다.<br/><br/>&bull; &nbsp; &nbsp; `SQL_COPT_SS_TRUSTEDCMKPATHS`를 사용하여 애플리케이션이 Always Encrypted 작업에서 열 마스터 키의 지정된 목록만 사용하도록 제한할 수 있습니다.<br/><br/>[SQL Server용 ODBC 드라이버와 함께 Always Encrypted 사용](../using-always-encrypted-with-the-odbc-driver.md)을 참조하세요. |
| 기본 위치에서 `.rll` 로드 지원. | [설치 설명서의 '리소스 파일 로드' 섹션](installing-the-microsoft-odbc-driver-for-sql-server.md#resource-file-loading)을 참조하세요. |
| 버그 수정. | [버그 수정](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="17"></a>17

**지원되는 새 배포**: macOS High Sierra 및 Ubuntu 17.10 

**향상된 성능**: 드라이버가 UTF-8/16으로 또는 UTF-8/16에서 변환하는 경우 성능이 10배 이상 개선됩니다.

**추가된 기능**:

BCP API에 대한 Always Encrypted 지원

새 연결 문자열 속성 UseFMTOnly는 임시 테이블이 필요한 특별한 경우 드라이버에서 구형 메타데이터를 사용하게 합니다.

Azure SQL Managed Instance 지원. 
> [!NOTE]
> Managed Instance를 사용하는 경우 여러 가지 차이점이 있습니다.
> -   FILESTREAM이 지원되지 않음 
> -   로컬 파일 시스템 액세스는 지원되지 않지만 추적 파일과 같은 사항을 위해 필요함 
> -   로컬 경로에서 UDT 만들기는 지원되지 않음 
> -   Windows 통합 인증은 지원되지 않음 
> -   DTC는 지원되지 않습니다. 
> -   'sa' 계정이 없음(기본 계정을 'cloudSA'라 함)
> -   TDS 토큰 ERROR(0xAA)가 잘못된 서버 이름을 반환함
> -   데이터베이스 이름에 특수 문자가 지원되지 않음 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2]가 지원되지 않음
> -   오류 메시지는 언어 설정(Azure와 동일)에 관계 없이 항상 영어로 표시됨 

## <a name="131-for-ssnoversion-on-linux-and-macos-may-2017"></a>13.1, Linux 및 macOS 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 경우, 2017년 5월

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 ODBC 드라이버 13.1은 Microsoft SQL Server 2016과 함께 사용하는 경우 Always Encrypted 및 Azure Active Directory ODBC 드라이버 지원을 추가합니다.

**지원되는 새 배포.** : OS X 10.11 및 macOS 10.12는 macOS 기반 ODBC 드라이버의 첫 번째 릴리스에서 지원됩니다. 이제 Red Hat 6, 7 및 SUSE 12와 함께 Ubuntu 16.10도 지원됩니다. 각 플랫폼에는 설치 및 구성을 용이하게 해주기 위한 플랫폼 관련 패키지(RPM 또는 DEB)가 있습니다. 자세한 내용은 [Linux](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) 및 [macOS](../../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md)의 ODBC 드라이버 설치 지침을 참조하세요.

**unixODBC 드라이버 관리자 2.3.1 지원 변경 사항**: ODBC 드라이버는 더 이상 unixODBC 드라이버 관리자용 사용자 지정 패키징(RedHat 6의 경우 제외)에 의존하지 않으며, 배포 패키지 관리자에 의존하여 배포의 리포지토리에서 UnixODBC 종속성을 해결합니다.

**BCP API 지원**: Linux 및 macOS ODBC 드라이버는 이제 [BCP API 함수(**bcp_init** 등)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md) 사용을 지원합니다.

## <a name="130-for-ssnoversion-on-linux"></a>13.0, Linux 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 경우

이제 Microsoft ODBC Driver 13.0 for SQL Server, SQL Server 2014 및 SQL Server 2016도 지원됩니다.  

**지원되는 새 배포.** :

이제 Ubuntu가 Red Hat 및 SUSE와 함께 지원됩니다. 각 플랫폼에는 설치 및 구성을 용이하게 해주기 위한 플랫폼 관련 패키지(RPM 또는 DEB)가 있습니다.  설치 지침은 [드라이버 설치](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)를 참조하세요.

**unixODBC 드라이버 관리자 2.3.1 지원**: 최신 드라이버 관리자뿐만 아니라 설치 및 구성을 용이하게 해주는 이 종속성을 설치하기 위한 패키지도 있습니다.  

**투명 네트워크 IP 확인**: 투명한 네트워크 IP 확인은 호스트 이름의 첫 번째 확인된 IP가 응답하지 않고 해당 호스트 이름과 연결된 복수의 IP가 있는 경우 드라이버의 연결 순서에 영향을 주는 기존 다중 서브넷 장애 조치(failover) 기능의 개정판입니다.

**TLS 1.2 지원**: Linux 기반 Microsoft ODBC Driver 13.0 for SQL Server는 이제 SQL Server와의 보안 통신을 사용하는 경우 TLS 1.2를 지원합니다.

## <a name="11-for-ssnoversion-on-linux"></a>11, Linux 기반 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 경우

SUSE Linux(Preview)의 ODBC 드라이버는 64비트 SUSE Linux Enterprise 11 서비스 팩 2를 지원합니다. 자세한 내용은 [System Requirements](../../../connect/odbc/linux-mac/system-requirements.md)을 참조하세요.  

Linux 기반 ODBC 드라이버는 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]을 지원합니다. 자세한 내용은 [고가용성, 재해 복구를 위한 Linux 기반 ODBC 드라이버 지원](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)을 참조하세요.  

Linux 기반 ODBC 드라이버는 Azure SQL Database에 대한 연결을 지원합니다.

`bcp`에 `-l` 옵션(로그인 시간 제한)이 추가되었습니다. 자세한 내용은 [Connecting with **bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md)을 참조하세요.
