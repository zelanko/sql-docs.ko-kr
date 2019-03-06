---
title: 릴리스 정보(SQL Server용 OLE DB 드라이버)| Microsoft Docs
ms.date: 02/12/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
ms.openlocfilehash: 36dc1b7325265da6231b75e9f4db46854b0b219f
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744363"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>SQL Server용 Microsoft OLE DB 드라이버에 대한 릴리스 정보
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

이 페이지에서는 SQL Server 용 Microsoft OLE DB 드라이버의 각 버전에 추가 된 기능에 대해 설명 합니다.

## <a name="whats-new-in-version-1821"></a>버전 18.2.1의 새로운 기능

**추가 기능은 다음과 같습니다.**

* 서버 인코딩 u t F-8을 지원 합니다. 자세한 내용은 참조 하십시오: [OLE DB 드라이버에서 SQL Server에 대 한 u t F-8 지원](features/utf-8-support-in-oledb-driver-for-sql-server.md)합니다.
* Azure Active Directory 인증 지원. 자세한 내용은 [Azure Active Directory 사용](features/using-azure-active-directory.md)을 참조하세요.

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
