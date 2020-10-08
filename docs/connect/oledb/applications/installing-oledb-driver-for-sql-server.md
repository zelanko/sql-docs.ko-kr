---
title: SQL Server용 OLE DB 드라이버 설치 | Microsoft Docs
description: OLE DB Driver for SQL Server 설치 및 제거 OLE DB Driver for SQL Server를 설치하려면 msoledbsql.msi 설치 프로그램이 필요합니다.
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, uninstalling
- MSOLEDBSQL, installing
- MSOLEDBSQL, uninstalling
- Setup [OLE DB Driver for SQL Server]
- uninstalling OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], uninstalling OLE DB Driver for SQL Server
- installing OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, installing
- data access [OLE DB Driver for SQL Server], installing OLE DB Driver for SQL Server
- removing OLE DB Driver for SQL Server
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 43b91e08726ed548d24ba3461f45164eb97bb6b7
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727374"
---
# <a name="installing-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버 설치
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

OLE DB Driver for SQL Server를 설치하려면 msoledbsql.msi 설치 프로그램이 필요합니다.
설치 프로그램을 실행하고 원하는 대로 설정합니다. OLE DB Driver for SQL Server는 이전 버전의 Microsoft OLE DB 공급자가 설치된 상태에서 설치할 수 있습니다.

OLE DB Driver for SQL Server 파일(msoledbsql.dll, msoledbsqlr.rll)은 `%SYSTEMROOT%\system32\`에 설치됩니다. 또한 x64 msoledbsql.msi는 `%SYSTEMROOT%\SysWOW64\`에 32비트 이진 파일을 설치합니다.

> [!NOTE]  
> OLE DB Driver for SQL Server에 대한 모든 적절한 레지스트리 설정은 설치 프로세스 과정에서 수행됩니다.  

OLE DB Driver for SQL Server 헤더 및 라이브러리 파일(msoledbsql.h 및 msoledbsql.lib)은 `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`에 설치됩니다. 또한 x64 msoledbsql.msi는 `%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`에 동일한 파일을 설치합니다.  

msoledbsql.msi를 통해 OLE DB Driver for SQL Server를 배포할 수 있습니다. 애플리케이션을 배포할 때 OLE DB Driver for SQL Server를 설치해야 할 수도 있습니다. 여러 패키지를 단일 설치인 것처럼 보이게 설치하려는 경우 chainer와 부트스트래퍼 기술을 사용하는 것이 하나의 방법이 될 수 있습니다. 자세한 내용은 [Visual Studio 2005용 사용자 지정 부트스트래퍼 패키지 제작](/previous-versions/aa730839(v=vs.80)) 및 [사용자 지정 필수 구성 요소 추가](/visualstudio/deployment/creating-bootstrapper-packages)를 참조하십시오.  
  
또한 x64 msoledbsql.msi는 32비트 버전의 OLE DB Driver for SQL Server를 설치합니다. 애플리케이션을 처음에 개발된 플랫폼이 아닌 다른 플랫폼에서 사용하려는 경우 x64 및 x86용 msoledbsql.msi 버전을 다운로드할 수 있습니다.

msoledbsql.msi를 호출하면 클라이언트 구성 요소만 기본적으로 설치됩니다. 클라이언트 구성 요소는 SQL Server용 OLE DB 드라이버를 사용하여 개발된 애플리케이션을 실행하는 데 필요한 파일입니다. SDK 구성 요소도 함께 설치하려면 명령줄에 `ADDLOCAL=All`을 지정하면 됩니다. 다음은 그 예입니다.  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>자동 설치  
 msiexec 명령에 /passive, /qn, /qb, or /qr 옵션을 사용할 경우 IACCEPTMSOLEDBSQLLICENSETERMS=YES를 지정하여 최종 사용자 사용권 약관에 동의함을 명시적으로 나타내야 합니다. 이 옵션은 모두 대문자로 지정해야 합니다.  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>OLE DB Driver for SQL Server를 종속성으로 설치  
모든 종속 애플리케이션을 제거할 때까지는 OLE DB Driver for SQL Server를 제거하지 않는 것이 중요합니다. 애플리케이션이 OLE DB Driver for SQL Server에 종속되어 있다는 경고를 사용자에게 표시하려면 다음과 같이 MSI에 APPGUID 설치 옵션을 사용합니다.  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

APPGUID에는 제품 코드를 전달해야 합니다. 제품 코드는 Microsoft 설치 관리자를 사용하여 애플리케이션 설치 프로그램 번들을 작성할 때 만들어야 합니다.
APPGUID 옵션을 사용하려면 관리자 권한 명령 프롬프트에서 설치 관리자를 실행해야 합니다.

## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버로 애플리케이션 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)