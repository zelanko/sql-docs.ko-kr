---
title: SQL Server용 OLE DB 드라이버 설치 | Microsoft Docs
description: 설치 하 고 SQL Server 용 OLE DB 드라이버를 제거 합니다.
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
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: e779d51f535d3b3489c1fbe043c7ff9212b0e875
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800882"
---
# <a name="installing-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버 설치
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

SQL Server 용 OLE DB 드라이버를 설치 하려면 msoledbsql.msi 설치를 해야 합니다.
설치 관리자를 실행 하 고 기본 선택 항목을 확인 합니다. OLE DB Driver for SQL Server 이전 버전의 Microsoft OLE DB 공급자와 함께 설치 될 수 있습니다.

OLE DB Driver for SQL Server 파일 (msoledbsql.dll, msoledbsqlr.rll)에 설치 된 `%SYSTEMROOT%\system32\` 합니다. 또한 msoledbsql.msi의 32 비트 이진 파일을 설치 하는 x64 `%SYSTEMROOT%\SysWOW64\`합니다.

> [!NOTE]  
> SQL Server 용 OLE DB 드라이버에 대 한 모든 적절 한 레지스트리 설정은 설치 프로세스의 일부로 설정 됩니다.  

OLE DB Driver for SQL Server 헤더 및 라이브러리 파일 (msoledbsql.h 및 msoledbsql.lib)에 설치 된 `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`합니다. 또한 msoledbsql.msi 설치의 동일한 파일에 x64 `%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`합니다.  

Msoledbsql.msi 통해 SQL Server 용 OLE DB 드라이버를 배포할 수 있습니다. 응용 프로그램을 배포 하는 경우 SQL Server 용 OLE DB 드라이버를 설치 해야 합니다. 여러 패키지를 단일 설치인 것처럼 보이게 설치하려는 경우 chainer와 부트스트래퍼 기술을 사용하는 것이 하나의 방법이 될 수 있습니다. 자세한 내용은 [Visual Studio 2005용 사용자 지정 부트스트래퍼 패키지 제작](https://go.microsoft.com/fwlink/?LinkId=115667) 및 [사용자 지정 필수 구성 요소 추가](https://go.microsoft.com/fwlink/?LinkId=115668)를 참조하십시오.  
  
X64 msoledbsql.msi도 SQL Server 용 OLE DB 드라이버의 32 비트 버전을 설치 합니다. 응용 프로그램에 개발 된 것 이외의 플랫폼을 대상으로 하는 경우에 x64 및 x86 msoledbsql.msi의 버전을 다운로드할 수 있습니다.

msoledbsql.msi를 호출하면 클라이언트 구성 요소만 기본적으로 설치됩니다. 클라이언트 구성 요소는 SQL Server용 OLE DB 드라이버를 사용하여 개발된 애플리케이션을 실행하는 데 필요한 파일입니다. SDK 구성 요소도 함께 설치하려면 명령줄에 `ADDLOCAL=All`을 지정하면 됩니다. 예를 들어  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>자동 설치  
 msiexec 명령에 /passive, /qn, /qb, or /qr 옵션을 사용할 경우 IACCEPTMSOLEDBSQLLICENSETERMS=YES를 지정하여 최종 사용자 사용권 약관에 동의함을 명시적으로 나타내야 합니다. 이 옵션은 모두 대문자로 지정해야 합니다.  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>종속성으로 SQL Server 용 OLE DB 드라이버 설치  
것이 중요 하지 않습니다 모든 종속 응용 프로그램은 제거 될 때까지 SQL Server 용 OLE DB 드라이버를 제거 합니다. 사용자는 프로그램이 OLE DB 드라이버에서 SQL Server에 대 한 경고를 제공 하려면 MSI에 APPGUID 설치 옵션을 다음과 같이 사용 합니다.  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

APPGUID에는 제품 코드를 전달해야 합니다. 제품 코드는 Microsoft 설치 관리자를 사용하여 애플리케이션 설치 프로그램 번들을 작성할 때 만들어야 합니다.
APPGUID 옵션을 관리자 권한 명령 프롬프트에서 설치 관리자를 실행 해야 합니다.

## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버로 애플리케이션 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
