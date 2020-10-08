---
title: OLE DB Driver 릴리스 정보
description: 이 릴리스 정보 문서에서는 Microsoft OLE DB Driver for SQL Server의 각 릴리스의 변경 사항을 설명합니다.
ms.date: 05/25/2020
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 2e957fdb91720c46f5065f4b671c14b757a7cb0f
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726941"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>SQL Server용 Microsoft OLE DB 드라이버에 대한 릴리스 정보

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 페이지에서는 SQL Server용 Microsoft OLE DB 드라이버의 각 버전에 추가된 기능에 대해 설명합니다.

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1840"></a>18.4.0
![다운로드](../../ssms/media/download-icon.png) [x64 설치 관리자 다운로드](https://go.microsoft.com/fwlink/?linkid=2129954)  
![다운로드](../../ssms/media/download-icon.png) [x86 설치 관리자 다운로드](https://go.microsoft.com/fwlink/?linkid=2131003)  

릴리스 날짜: 2020년 5월

검색된 언어가 아닌 다른 언어로 설치 관리자를 다운로드해야 하는 경우 다음과 같은 직접 링크를 사용할 수 있습니다.  
x64 드라이버의 경우: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x40a)  
x86 드라이버의 경우: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x40a)  

### <a name="features-added"></a>추가된 기능

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| TNIR(투명 네트워크 IP 확인) 지원 |[TNIR(투명 네트워크 IP 확인)](features/using-transparent-network-ip-resolution.md)|
| UTF-8 클라이언트 인코딩 지원 | [SQL Server용 OLE DB 드라이버에서 UTF-8 지원](features/utf-8-support-in-oledb-driver-for-sql-server.md) |

### <a name="bugs-fixed"></a>버그 수정

| 버그 수정 | 세부 정보 |
| :-------- | :------ |
| [ISequentialStream](/previous-versions/windows/desktop/ms718035(v=vs.85)) 인터페이스에서 다양한 버그 수정 | 멀티 바이트 코드 페이지에 영향을 주는 몇 가지 버그 때문에 읽기 작업 중에 인터페이스가 도중에 스트림 끝을 보고했었습니다.|
| [IOpenRowset::OpenRowset](/previous-versions/windows/desktop/ms716724(v=vs.85)) 인터페이스에서 메모리 누수 문제 수정 | `SSPROP_IRowsetFastLoad` 속성이 사용하도록 설정된 경우 [IOpenRowset::OpenRowset](/previous-versions/windows/desktop/ms716724(v=vs.85)) 인터페이스에서 발생한 메모리 누수 문제가 수정되었습니다. |
| `sql_variant` 데이터 형식 및 비 ASCII 문자열을 포함하는 시나리오의 버그가 수정되었습니다. | `sql_variant` 데이터 형식 및 비 ASCII 문자열과 관련된 특정 시나리오를 실행하면 데이터가 손상될 수 있습니다. 자세한 내용은 다음을 참조하세요. [알려진 문제](ole-db-data-types/ssvariant-structure.md#known-issues). |
| [UDL 구성 대화 상자](help-topics/data-link-pages.md)에서 연결 테스트 단추 문제 해결 | [UDL 구성 대화 상자](help-topics/data-link-pages.md)의 연결 테스트 단추가 이제 모든 탭에서 설정된 초기화 속성을 인식합니다. |
| `SSPROP_INIT_PACKETSIZE` 속성 기본값 처리 수정 | `SSPROP_INIT_PACKETSIZE` 속성이 기본값 `0`으로 설정된 경우 발생하는 예기치 않은 오류가 수정되었습니다. 이 속성에 대한 자세한 내용은 [초기화 및 권한 부여 속성](ole-db-data-source-objects/initialization-and-authorization-properties.md)을 참조하세요. |
| [IBCPSession](ole-db-interfaces/ibcpsession-ole-db.md)에서 버퍼 오버플로 문제 수정 | 형식이 잘못된 데이터 파일을 사용하는 경우 발생한 버퍼 오버플로 문제가 해결되었습니다. |
| 접근성 문제 해결 | 설치 관리자 UI 및 [SQL Server 로그인 대화 상자](help-topics/sql-server-login-dialog.md)에서 접근성 문제가 해결되었습니다(내용 읽기, 탭 중지). |

## <a name="previous-releases"></a>이전 릴리스

## <a name="1830"></a>18.3.0

![다운로드](../../ssms/media/download-icon.png) [x64 설치 관리자 다운로드](https://go.microsoft.com/fwlink/?linkid=2117515)  
![다운로드](../../ssms/media/download-icon.png) [x86 설치 관리자 다운로드](https://go.microsoft.com/fwlink/?linkid=2117517)  

릴리스 날짜: 2019년 10월

검색된 언어가 아닌 다른 언어로 설치 관리자를 다운로드해야 하는 경우 다음과 같은 직접 링크를 사용할 수 있습니다.  
x64 드라이버의 경우: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x40a)  
x86 드라이버의 경우: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x40a)  

### <a name="features-added"></a>추가된 기능

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| Azure Active Directory 인증 지원(`ActiveDirectoryInteractive`, `ActiveDirectoryMSI`). | [Azure Active Directory 사용](features/using-azure-active-directory.md). |
| 설치 프로그램에 Azure ADAL(Active Directory 인증 라이브러리)(adal.dll) 포함 | 이제 기본 드라이버 설치에 포함되는 OLE DB 설치 관리자는 SQL Server용 Microsoft Active Directory 인증 라이브러리의 기존 설치를 업그레이드하고 Windows의 설치된 애플리케이션 목록에서 제거합니다. |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>버그 수정

| 버그 수정 | 세부 정보 |
| :-------- | :------ |
| [IIndexDefinition::DropIndex](/previous-versions/windows/desktop/ms722733(v=vs.85))의 인덱스 삭제 논리를 수정했습니다. | 이전 버전의 OLE DB 드라이버는 스키마 ID와 인덱스 소유자의 사용자 ID가 서로 다르면 기본 키 인덱스를 삭제할 수 없습니다. |
| &nbsp; | &nbsp; |

다음 섹션의 다운로드 링크를 클릭하여 이전 OLE DB 드라이버 버전을 다운로드하세요.

## <a name="1823"></a>18.2.3

![다운로드](../../ssms/media/download-icon.png) [x64 설치 관리자 다운로드](https://go.microsoft.com/fwlink/?linkid=2119554)  
![다운로드](../../ssms/media/download-icon.png) [x86 설치 관리자 다운로드](https://go.microsoft.com/fwlink/?linkid=2119738)  

릴리스 날짜: 2019년 6월

검색된 언어가 아닌 다른 언어로 설치 관리자를 다운로드해야 하는 경우 다음과 같은 직접 링크를 사용할 수 있습니다.  
x64 드라이버의 경우: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x40a)  
x86 드라이버의 경우: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x40a)  

### <a name="features-added-in-1823"></a>18.2.3에서 추가된 기능

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| SQL Server 이동식 미디어에서 드라이버 업그레이드를 지원합니다. | 이러한 개선으로 SQL Server 이동식 미디어에서 드라이버를 직접 업그레이드할 수 있습니다. |
| &nbsp; | &nbsp; |

## <a name="1822"></a>18.2.2

![다운로드](../../ssms/media/download-icon.png) [x64 설치 관리자 다운로드](https://go.microsoft.com/fwlink/?linkid=2118512)  
![다운로드](../../ssms/media/download-icon.png) [x86 설치 관리자 다운로드](https://go.microsoft.com/fwlink/?linkid=2118415)  

릴리스 날짜: 2019년 5월

검색된 언어가 아닌 다른 언어로 설치 관리자를 다운로드해야 하는 경우 다음과 같은 직접 링크를 사용할 수 있습니다.  
x64 드라이버의 경우: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x40a)  
x86 드라이버의 경우: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x40a)  

### <a name="bugs-fixed-in-1822"></a>18.2.2에서 수정된 버그

| 버그 수정 | 세부 정보 |
| :-------- | :------ |
| MTA(다중 스레드 아파트)에서 비 대화형 Azure Active Directory 인증이 수정되었습니다. | OLE DB 드라이버 18.2.1은 이전에 다중 스레드(MTA)로 초기화된 아파트에서 COM 동시성 모델을 잘못 변경하려고 시도합니다. 결과적으로, [IDBInitialize::Initialize](/previous-versions/windows/desktop/ms718026(v=vs.85)) 인터페이스를 호출하기 전에 [CoInitialize](/windows/win32/api/objbase/nf-objbase-coinitialize) 또는 [CoInitializeEx](/windows/win32/api/combaseapi/nf-combaseapi-coinitializeex)에 두 번 이상 후속 호출을 하는 애플리케이션에서 Azure Active Directory 인증 모드 중 하나를 사용할 때 드라이버가 연결되지 않습니다. |
| &nbsp; | &nbsp; |

## <a name="1821"></a>18.2.1

![다운로드](../../ssms/media/download-icon.png) [x64 설치 관리자 다운로드](https://go.microsoft.com/fwlink/?linkid=2118511)  
![다운로드](../../ssms/media/download-icon.png) [x86 설치 관리자 다운로드](https://go.microsoft.com/fwlink/?linkid=2118278)  

릴리스 날짜: 2019년 2월

검색된 언어가 아닌 다른 언어로 설치 관리자를 다운로드해야 하는 경우 다음과 같은 직접 링크를 사용할 수 있습니다.  
x64 드라이버의 경우: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x40a)  
x86 드라이버의 경우: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x40a)  

### <a name="features-added-in-1821"></a>18.2.1에서 추가된 기능

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| UTF-8 서버 인코딩 지원. | [OLE DB Driver for SQL Server에서 UTF-8 지원](features/utf-8-support-in-oledb-driver-for-sql-server.md), |
| Azure Active Directory 인증 지원. | [Azure Active Directory 사용](features/using-azure-active-directory.md). |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

![다운로드](../../ssms/media/download-icon.png) [x64 설치 관리자 다운로드](https://go.microsoft.com/fwlink/?linkid=2118506)  
![다운로드](../../ssms/media/download-icon.png) [x86 설치 관리자 다운로드](https://go.microsoft.com/fwlink/?linkid=2118509)  

릴리스 날짜: 2018년 7월

검색된 언어가 아닌 다른 언어로 설치 관리자를 다운로드해야 하는 경우 다음과 같은 직접 링크를 사용할 수 있습니다.  
x64 드라이버의 경우: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x40a)  
x86 드라이버의 경우: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2118509&2118509=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x40a)  

### <a name="features-added-in-1810"></a>18.1.0에서 추가된 기능

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| `UseFMTONLY` 연결 문자열 키워드 및 `SSPROP_INIT_USEFMTONLY` 초기화 속성에 대해 지원합니다. | `UseFMTONLY`는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상에 연결할 때 메타데이터를 검색하는 방법을 제어합니다.<br/><br/>자세한 내용은 다음을 참조하세요. [SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed-in-1810"></a>18.1.0에서 수정된 버그

| 버그 수정 | 세부 정보 |
| :-------- | :------ |
| BCP 형식 파일의 잘못된 버전이 수정되었습니다. | OLE DB 드라이버 18.0은 BCP 형식 파일의 버전을 11.0 대신 18.0으로 잘못 설정합니다.<br/>OLE DB 드라이버 18.0에서 생성된 형식 파일은 OLE DB 드라이버 18.1에서 읽을 수 없습니다.<br/>새 드라이버와 함께 이전 버전에서 생성된 서식 파일을 사용해야 하는 경우 수동으로 파일을 편집하여 버전을 11.0으로 변경할 수 있습니다. |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

![다운로드](../../ssms/media/download-icon.png) [x64 설치 관리자 다운로드](https://go.microsoft.com/fwlink/?linkid=2118504)  
![다운로드](../../ssms/media/download-icon.png) [x86 설치 관리자 다운로드](https://go.microsoft.com/fwlink/?linkid=2118277)  

릴리스 날짜: 2018년 3월

검색된 언어가 아닌 다른 언어로 설치 관리자를 다운로드해야 하는 경우 다음과 같은 직접 링크를 사용할 수 있습니다.  
x64 드라이버의 경우: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x40a)  
x86 드라이버의 경우: [중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x40a)  

### <a name="features-added-in-1802"></a>18.0.2에서 추가된 기능

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| `MultiSubnetFailover` 연결 문자열 키워드 및 `SSPROP_INIT_MULTISUBNETFAILOVER` 초기화 속성을 지원합니다. | 자세한 내용은 다음을 참조하세요.<br/>&bull; &nbsp; [OLE DB Driver for SQL Server의 고가용성, 재해 복구 지원](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).<br/>&bull; &nbsp; [SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>참고 항목

[SQL Server용 Microsoft OLE DB 드라이버](oledb-driver-for-sql-server.md)