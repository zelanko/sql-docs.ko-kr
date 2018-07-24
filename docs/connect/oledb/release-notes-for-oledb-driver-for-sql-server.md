---
title: 릴리스 정보 (OLE DB Driver for SQL Server) | Microsoft Docs
ms.date: 07/03/2018
ms.prod: sql
ms.suite: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
ms.openlocfilehash: ec5abfce888f0af956f1b72f509ef298ee7405a0
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39109375"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>SQL Server용 Microsoft OLE DB 드라이버에 대한 릴리스 정보
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

이 페이지에서는 SQL Server 용 Microsoft OLE DB 드라이버의 각 버전에 추가 된 기능에 대해 설명 합니다.

## <a name="whats-new-in-version-1810"></a>버전 18.1.0의 새로운 기능

**추가 기능은 다음과 같습니다.**

* 에 대 한 지원 `UseFMTONLY` 연결 문자열 키워드 및 `SSPROP_INIT_USEFMTONLY` 초기화 속성입니다.
`UseFMTONLY` 메타 데이터에 연결할 때 검색 되는 방법을 제어 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상.  
참조 항목:
  * [SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)

**수정 된 버그:**

* BCP 형식 파일의 잘못 된 버전을 고정된 합니다. OLE DB 드라이버 18.0 제대로 설정 하지 BCP 형식 파일의 버전 11.0 대신 18.0을 합니다. OLE DB 드라이버 18.1에서 OLE DB 드라이버 18.0에서 생성 된 서식 파일을 읽을 수 없습니다. 새 드라이버를 사용 하 여 이전 버전에서 생성 된 서식 파일을 사용 하는 경우 버전 11.0을 변경 하려면 파일을 수동으로 편집할 수 있습니다.

## <a name="whats-new-in-version-1802"></a>버전 18.0.2의 새로운 기능

**추가 기능**:

* 에 대 한 지원 `MultiSubnetFailover` 연결 문자열 키워드 및 `SSPROP_INIT_MULTISUBNETFAILOVER` 초기화 속성입니다.  
참조 항목:  
  * [SQL Server용 OLE DB 드라이버의 고가용성, 재해 복구 지원](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
  * [SQL Server용 OLE DB 드라이버에서 연결 문자열 키워드 사용](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)

## <a name="see-also"></a>관련 항목:
[SQL Server용 Microsoft OLE DB 드라이버](oledb-driver-for-sql-server.md)
