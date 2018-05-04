---
title: SQL Server 용 OLE DB 드라이버를 설치 합니다. | Microsoft Docs
description: 설치 및 OLE DB Driver for SQL Server 제거
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 3cb05e6fbbc3507aec67f4faa61f621c4245e7c8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="installing-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 설치
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

SQL Server 용 OLE DB 드라이버를 설치 하려면 msoledbsql.msi 설치를 해야 합니다.
설치 프로그램을 실행 하 고 기본 선택 항목을 확인 합니다. OLE DB Driver for SQL Server 이전 버전의 Microsoft OLE DB 공급자와 함께 설치할된 수 있습니다.

OLE DB 드라이버에서 SQL Server 파일 (msoledbsql.dll, msoledbsqlr.rll)에 설치 된 `%SYSTEMROOT%\system32\` 합니다. 또한 msoledbsql.msi에서 32 비트 이진 파일을 설치 하는 x64 `%SYSTEMROOT%\SysWOW64\`합니다.

> [!NOTE]  
> SQL Server 용 OLE DB Driver에 대 한 모든 적절 한 레지스트리 설정은 설치 과정의 일환으로 이루어집니다.  

OLE DB 드라이버에서 SQL Server 헤더 및 라이브러리 파일 (msoledbsql.h 및 msoledbsql.lib)에 설치 된 `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\180\SDK`합니다. 또한 msoledbsql.msi에서 동일한 파일을 설치 하는 x64 `%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\180\SDK`합니다.  

Msoledbsql.msi를 통해 SQL Server 용 OLE DB 드라이버를 배포할 수 있습니다. 응용 프로그램을 배포할 때 SQL Server 용 OLE DB 드라이버를 설치 해야 합니다. 여러 패키지를 단일 설치인 것처럼 보이게 설치하려는 경우 chainer와 부트스트래퍼 기술을 사용하는 것이 하나의 방법이 될 수 있습니다. 자세한 내용은 참조 [Visual Studio 2005 용 사용자 지정 부트스트래퍼 패키지 제작](http://go.microsoft.com/fwlink/?LinkId=115667) 및 [사용자 지정 필수 구성 요소 추가](http://go.microsoft.com/fwlink/?LinkId=115668)합니다.  
  
X64 msoledbsql.msi SQL Server를 32 비트 버전의 OLE DB 드라이버를 설치 됩니다. 응용 프로그램에 개발 된 것과 다른 플랫폼을 대상 경우 msoledbsql.msi x64 및 x86 버전을 다운로드할 수 있습니다.

Msoledbsql.msi를 호출할 때 클라이언트 구성 요소만 기본적으로 설치 됩니다. 구성 요소는 클라이언트는 SQL Server 용 OLE DB 드라이버를 사용 하 여 개발 된 응용 프로그램을 실행 하는 데 파일입니다. SDK 구성 요소도 함께 설치하려면 명령줄에 `ADDLOCAL=All`을 지정하면 됩니다. 예를 들어:  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>자동 설치  
 Msiexec와 /passive, /qn, /qb, 또는 /qr 옵션을 사용 하는 경우 IACCEPTMSOLEDBSQLLICENSETERMS 지정 해야 = 예, 나타내려면 명시적으로 최종 사용자 사용권 계약 조건에 동의 합니다. 이 옵션은 모두 대문자로 지정해야 합니다.  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>종속 항목으로 OLE DB Driver for SQL Server 설치  
모든 종속 된 응용 프로그램이 제거 될 때까지 SQL Server 용 OLE DB 드라이버를 제거 하지는 것이 유용 합니다. 사용자가 응용 프로그램이 SQL Server 용 OLE DB 드라이버에 종속 되도록 경고를 제공 하려면 MSI에 APPGUID 설치 옵션을 다음과 같이 사용 합니다.  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

APPGUID에는 제품 코드를 전달해야 합니다. 제품 코드는 Microsoft 설치 관리자를 사용하여 응용 프로그램 설치 프로그램 번들을 작성할 때 만들어야 합니다.
APPGUID 옵션을 사용 하려면 관리자 권한 명령 프롬프트에서 설치 프로그램을 실행 합니다.

## <a name="see-also"></a>관련 항목:  
 [SQL Server용 OLE DB 드라이버로 응용 프로그램 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
