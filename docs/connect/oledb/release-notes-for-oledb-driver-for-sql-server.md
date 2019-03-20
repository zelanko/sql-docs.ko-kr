---
title: 릴리스 정보(SQL Server용 OLE DB 드라이버)| Microsoft Docs
ms.date: 02/13/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 2a1d6d216f4f7ec7fee0f5f9aa5810c78f1936e6
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161770"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>SQL Server용 Microsoft OLE DB 드라이버에 대한 릴리스 정보

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

이 페이지에서는 SQL Server 용 Microsoft OLE DB 드라이버의 각 버전에 추가 된 기능에 대해 설명 합니다.

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1821"></a>18.2.1

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

2019년 2월

### <a name="features-added"></a>추가 기능

| 추가 된 기능 | 세부 정보 |
| :------------ | :------ |
| 서버 인코딩 u t F-8을 지원 합니다. | &bull; &nbsp; [SQL Server용 OLE DB 드라이버에서 UTF-8 지원](features/utf-8-support-in-oledb-driver-for-sql-server.md). |
| Azure Active Directory 인증 지원. | &bull; &nbsp; [Azure Active Directory 사용](features/using-azure-active-directory.md). |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

2018년 7월

### <a name="features-added"></a>추가 기능

| 추가 된 기능 | 세부 정보 |
| :------------ | :------ |
| 에 대 한 지원 합니다 `UseFMTONLY` 연결 문자열 키워드 및는 `SSPROP_INIT_USEFMTONLY` 초기화 속성입니다. | `UseFMTONLY` 메타 데이터에 연결할 때 검색 되는 방법을 제어 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상.<br/><br/>&bull; &nbsp; [SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>수정 된 버그

| 버그 수정 | 세부 정보 |
| :-------- | :------ |
| BCP 형식 파일의 잘못 된 버전을 고정된 합니다. | OLE DB 드라이버 18.0 올바르게 설정 되지 18.0, BCP 형식 파일의 버전 대신 11.0입니다.<br/><br/>OLE DB 드라이버 18.1에서 OLE DB 드라이버 18.0에서 생성 된 서식 파일을 읽을 수 없습니다.<br/><br/>새 드라이버를 사용 하 여 이전 버전에서 생성 된 서식 파일을 사용 하는 경우 버전 11.0을 변경 하려면 파일을 수동으로 편집할 수 있습니다. |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

### <a name="features-added"></a>추가 기능

| 추가 된 기능 | 세부 정보 |
| :------------ | :------ |
| 에 대 한 지원 합니다 `MultiSubnetFailover` 연결 문자열 키워드 및 `SSPROP_INIT_MULTISUBNETFAILOVER` 초기화 속성입니다. | &bull; &nbsp; [SQL Server용 OLE DB 드라이버의 고가용성, 재해 복구 지원](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).<br/><br/>&bull; &nbsp; [SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>관련 항목:

[SQL Server용 Microsoft OLE DB 드라이버](oledb-driver-for-sql-server.md)
