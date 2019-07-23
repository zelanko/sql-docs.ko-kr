---
title: SQL Server용 OLE DB 드라이버 설치 | Microsoft Docs
description: SQL Server에 대 한 OLE DB 드라이버 설치 및 제거
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
ms.openlocfilehash: 08f33d84ee8c035e1e1d3818e2a036f96af2a280
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989314"
---
# <a name="installing-ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버 설치
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

SQL Server에 대 한 OLE DB 드라이버를 설치 하려면 msoledbsql 설치 관리자가 필요 합니다.
설치 관리자를 실행 하 고 원하는 대로 선택 합니다. SQL Server에 대 한 OLE DB 드라이버는 이전 버전의 Microsoft OLE DB 공급자와 함께 설치할 수 있습니다.

SQL Server 파일 (msoledbsql, msoledbsqlr, rll 파일이)에 대 한 OLE DB 드라이버는에 `%SYSTEMROOT%\system32\` 설치 됩니다. 또한 x64 msoledbsql는에서 `%SYSTEMROOT%\SysWOW64\`32 비트 이진 파일을 설치 합니다.

> [!NOTE]  
> SQL Server의 OLE DB 드라이버에 대 한 모든 적절 한 레지스트리 설정은 설치 프로세스의 일부로 수행 됩니다.  

SQL Server 헤더 및 라이브러리 파일 (msoledbsql 및 msoledbsql)에 대 한 OLE DB 드라이버는에 `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`설치 됩니다. 또한 x64 msoledbsql는에 `%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`동일한 파일을 설치 합니다.  

Msoledbsql를 통해 SQL Server에 대 한 OLE DB 드라이버를 배포할 수 있습니다. 응용 프로그램을 배포할 때 SQL Server에 대 한 OLE DB 드라이버를 설치 해야 할 수도 있습니다. 여러 패키지를 단일 설치인 것처럼 보이게 설치하려는 경우 chainer와 부트스트래퍼 기술을 사용하는 것이 하나의 방법이 될 수 있습니다. 자세한 내용은 [Visual Studio 2005용 사용자 지정 부트스트래퍼 패키지 제작](https://go.microsoft.com/fwlink/?LinkId=115667) 및 [사용자 지정 필수 구성 요소 추가](https://go.microsoft.com/fwlink/?LinkId=115668)를 참조하십시오.  
  
또한 x64 msoledbsql는 SQL Server에 대 한 32 비트 버전의 OLE DB 드라이버를 설치 합니다. 응용 프로그램이 개발 된 플랫폼이 아닌 다른 플랫폼을 대상으로 하는 경우 x64 및 x86 용 msoledbsql의 버전을 다운로드할 수 있습니다.

msoledbsql.msi를 호출하면 클라이언트 구성 요소만 기본적으로 설치됩니다. 클라이언트 구성 요소는 SQL Server용 OLE DB 드라이버를 사용하여 개발된 애플리케이션을 실행하는 데 필요한 파일입니다. SDK 구성 요소도 함께 설치하려면 명령줄에 `ADDLOCAL=All`을 지정하면 됩니다. 예를 들어  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>자동 설치  
 msiexec 명령에 /passive, /qn, /qb, or /qr 옵션을 사용할 경우 IACCEPTMSOLEDBSQLLICENSETERMS=YES를 지정하여 최종 사용자 사용권 약관에 동의함을 명시적으로 나타내야 합니다. 이 옵션은 모두 대문자로 지정해야 합니다.  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>종속성으로 SQL Server에 대 한 OLE DB 드라이버를 설치 하는 중  
모든 종속 응용 프로그램이 제거 될 때까지 SQL Server OLE DB 드라이버를 제거 하지 않는 것이 중요 합니다. 응용 프로그램이 SQL Server에 대 한 OLE DB 드라이버에 의존 한다는 경고를 사용자에 게 제공 하려면 다음과 같이 MSI에서 APPGUID 설치 옵션을 사용 합니다.  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

APPGUID에는 제품 코드를 전달해야 합니다. 제품 코드는 Microsoft 설치 관리자를 사용하여 애플리케이션 설치 프로그램 번들을 작성할 때 만들어야 합니다.
APPGUID 옵션을 사용 하려면 관리자 권한 명령 프롬프트에서 설치 관리자를 실행 해야 합니다.

## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버로 애플리케이션 빌드](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
