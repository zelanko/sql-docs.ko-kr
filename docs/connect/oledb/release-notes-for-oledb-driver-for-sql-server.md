---
title: 릴리스 정보(SQL Server용 OLE DB 드라이버)| Microsoft Docs
ms.date: 05/13/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 969caa46506c9fd19410c5ace753076b3ba02fbe
ms.sourcegitcommit: 553ecea0427e4d2118ea1ee810f4a73275b40741
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65619989"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>SQL Server용 Microsoft OLE DB 드라이버에 대한 릴리스 정보

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

이 페이지에서는 SQL Server용 Microsoft OLE DB 드라이버의 각 버전에 추가된 기능에 대해 설명합니다.

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1822"></a>18.2.2

2019년 5월

### <a name="bugs-fixed"></a>버그 수정

| 버그 수정 | 세부 정보 |
| :-------- | :------ |
| MTA(다중 스레드 아파트)에서 비 대화형 Azure Active Directory 인증이 수정되었습니다. | OLE DB 드라이버 18.2.1은 이전에 다중 스레드(MTA)로 초기화된 아파트에서 COM 동시성 모델을 잘못 변경하려고 시도합니다. 결과적으로, [IDBInitialize::Initialize](https://go.microsoft.com/fwlink/?linkid=2092522) 인터페이스를 호출하기 전에 [CoInitialize](https://go.microsoft.com/fwlink/?linkid=2092520) 또는 [CoInitializeEx](https://go.microsoft.com/fwlink/?linkid=2092521)에 두 번 이상 후속 호출을 하는 애플리케이션에서 Azure Active Directory 인증 모드 중 하나를 사용할 때 드라이버가 연결되지 않습니다. |
| &nbsp; | &nbsp; |

## <a name="1821"></a>18.2.1

2019년 2월

### <a name="features-added"></a>추가된 기능

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| UTF-8 서버 인코딩 지원. | &bull; &nbsp; [SQL Server용 OLE DB 드라이버에서 UTF-8 지원](features/utf-8-support-in-oledb-driver-for-sql-server.md). |
| Azure Active Directory 인증 지원. | &bull; &nbsp; [Azure Active Directory 사용](features/using-azure-active-directory.md). |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

2018년 7월

### <a name="features-added"></a>추가된 기능

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| `UseFMTONLY` 연결 문자열 키워드 및 `SSPROP_INIT_USEFMTONLY` 초기화 속성에 대해 지원합니다. | `UseFMTONLY`는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상에 연결할 때 메타데이터를 검색하는 방법을 제어합니다.<br/><br/>&bull; &nbsp; [SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>버그 수정

| 버그 수정 | 세부 정보 |
| :-------- | :------ |
| BCP 형식 파일의 잘못된 버전이 수정되었습니다. | OLE DB 드라이버 18.0은 BCP 형식 파일의 버전을 11.0 대신 18.0으로 잘못 설정합니다.<br/><br/>OLE DB 드라이버 18.0에서 생성된 형식 파일은 OLE DB 드라이버 18.1에서 읽을 수 없습니다.<br/><br/>새 드라이버와 함께 이전 버전에서 생성된 서식 파일을 사용해야 하는 경우 수동으로 파일을 편집하여 버전을 11.0으로 변경할 수 있습니다. |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

### <a name="features-added"></a>추가된 기능

| 추가된 기능 | 세부 정보 |
| :------------ | :------ |
| `MultiSubnetFailover` 연결 문자열 키워드 및 `SSPROP_INIT_MULTISUBNETFAILOVER` 초기화 속성을 지원합니다. | &bull; &nbsp; [SQL Server용 OLE DB 드라이버의 고가용성, 재해 복구 지원](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).<br/><br/>&bull; &nbsp; [SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>관련 항목:

[SQL Server용 Microsoft OLE DB 드라이버](oledb-driver-for-sql-server.md)
