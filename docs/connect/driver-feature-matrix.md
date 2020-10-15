---
title: 드라이버 기능 지원 매트릭스
description: SQL Server용 드라이버에서 지원되는 인기 기능 및 해당 기능에 대한 정보를 찾을 수 있는 위치에 대해 알아봅니다.
ms.custom: ''
ms.date: 08/05/2020
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-daenge
ms.openlocfilehash: 6a781688b4fc24f8b79f3820fbcc3dc339b6c068
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081432"
---
# <a name="driver-feature-support-matrix-for-microsoft-sql-server"></a>Microsoft SQL Server용 드라이버 기능 지원 매트릭스

Microsoft SQL Server의 기능을 사용하려는 경우 일부 드라이버에서 사용하지 못할 수도 있습니다. 특정 드라이버에 기능이 없는 몇 가지 이유는 다음과 같습니다.

- 해당 기능이 특정 드라이버 기술에 적용되지 않습니다.
- 해당 기능이 새로운 기능이어서 아직 모든 드라이버에서 구현되지 않았습니다.
- 해당 기능이 특정 드라이버에서 필요하지 않습니다.
- 다른 기능을 먼저 구현하는 중입니다.

Microsoft에서는 모든 드라이버가 모든 기능을 지원하기를 희망하며 드라이버 간에 기능 패리티를 보장하기 위해 노력하고 있습니다. 그러나 이것이 항상 가능하지는 않습니다. 요구 사항에 적합한 드라이버를 선택하는 데 도움이 되도록 다음과 같이 인기 있는 기능 및 해당 기능을 구현하는 드라이버의 목록을 제공합니다.

- [.NET](#table1)
- [ODBC](#table2)
- [OLE DB](#table2)
- [JDBC](#table2)
- [PHP](#table3)
- [Node.js/JavaScript](#table3)
- [Python](#table3)

| <a id="table1"></a>기능 | [Microsoft.<wbr>Data.<wbr>SqlClient(.NET Core)](ado-net/microsoft-ado-net-sql-server.md) | [Microsoft.<wbr>Data.<wbr>SqlClient(.NET Framework)](ado-net/microsoft-ado-net-sql-server.md) | System.<wbr>Data.<wbr>SqlClient(.NET Core) | [System.<wbr>Data.<wbr>SqlClient(.NET Framework)](/dotnet/framework/data/adonet/sql/) |
| :-- | :-- | :-- | :-- | :-- |
| [Always Encrypted](../relational-databases/security/encryption/always-encrypted-database-engine.md) | [예](ado-net/sql/sqlclient-support-always-encrypted.md) | [예](ado-net/sql/sqlclient-support-always-encrypted.md) | | [예](ado-net/sql/sqlclient-support-always-encrypted.md) |
| [보안 enclave를 사용한 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md) | [예](ado-net/sql/sqlclient-support-always-encrypted.md#enabling-always-encrypted-with-secure-enclaves) | [예](ado-net/sql/sqlclient-support-always-encrypted.md#enabling-always-encrypted-with-secure-enclaves) | | [예](ado-net/sql/sqlclient-support-always-encrypted.md#enabling-always-encrypted-with-secure-enclaves) |
| [Azure Active Directory 액세스 토큰 인증](/azure/active-directory/develop/access-tokens) | [예](/dotnet/api/system.data.sqlclient.sqlconnection.accesstoken) | [예](/dotnet/api/microsoft.data.sqlclient.sqlconnection.accesstoken) | [예](/dotnet/api/microsoft.data.sqlclient.sqlconnection.accesstoken) | [예](/dotnet/api/microsoft.data.sqlclient.sqlconnection.accesstoken) |
| [Azure Active Directory 암호 인증](/azure/sql-database/sql-database-aad-authentication) | yes | yes | | 예 |
| [Azure Active Directory 통합 인증](/azure/sql-database/sql-database-aad-authentication) | yes | yes | | 예 |
| [Azure Active Directory 대화형(MFA) 인증](/azure/sql-database/sql-database-aad-authentication) | yes | yes | | 예 |
| [Azure Active Directory 관리 ID 인증](/azure/active-directory/managed-identities-azure-resources/overview) | | | | |
| [Azure Active Directory 서비스 사용자 인증](/azure/active-directory/develop/app-objects-and-service-principals) | yes | 예 | | |
| [Windows 통합 인증](/windows-server/security/windows-authentication/windows-authentication-overview) | [예](ado-net/sql/authentication-sql-server.md) | [예](ado-net/sql/authentication-sql-server.md) | [예](/dotnet/framework/data/adonet/sql/authentication-in-sql-server) | [예](/dotnet/framework/data/adonet/sql/authentication-in-sql-server) |
| [대량 복사](../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) | [예](ado-net/sql/bulk-copy-operations-sql-server.md) | [예](ado-net/sql/bulk-copy-operations-sql-server.md) | [예](/dotnet/framework/data/adonet/sql/bulk-copy-operations-in-sql-server) | [예](/dotnet/framework/data/adonet/sql/bulk-copy-operations-in-sql-server) |
| [데이터 민감도 및 분류 메타데이터](../relational-databases/security/sql-data-discovery-and-classification.md) | yes | yes | yes | 예 |
| [MARS(Multiple Active Result Sets)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [예](ado-net/sql/multiple-active-result-sets-mars.md) | [예](ado-net/sql/multiple-active-result-sets-mars.md) | [예](/dotnet/framework/data/adonet/sql/multiple-active-result-sets-mars) | [예](/dotnet/framework/data/adonet/sql/multiple-active-result-sets-mars) |
| [공간 데이터 형식](../relational-databases/spatial/spatial-data-sql-server.md) | | yes | | 예 |
| [TVP(테이블 반환 매개 변수)](../relational-databases/tables/use-table-valued-parameters-database-engine.md) | [예](ado-net/sql/table-valued-parameters.md) | [예](ado-net/sql/table-valued-parameters.md) | [예](/dotnet/framework/data/adonet/sql/table-valued-parameters) | [예](/dotnet/framework/data/adonet/sql/table-valued-parameters) |
| [MultiSubnetFailover](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [예](ado-net/sql/sqlclient-support-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [예](ado-net/sql/sqlclient-support-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [예](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.multisubnetfailover?view=netcore-1.0&preserve-view=true) | [예](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.multisubnetfailover?view=netframework-4.8&preserve-view=true) |
| [투명 네트워크 IP 확인](odbc/using-transparent-network-ip-resolution.md) | | [예](/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring?view=sqlclient-dotnet-1.1&preserve-view=true) | | [예](/dotnet/api/system.data.sqlclient.sqlconnection.connectionstring?view=netframework-4.8&preserve-view=true) |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

| <a id="table2"></a>기능 | [Windows 기반 ODBC Driver for SQL Server](odbc/microsoft-odbc-driver-for-sql-server.md) | [Linux 및 macOS 기반 ODBC Driver for SQL Server](odbc/microsoft-odbc-driver-for-sql-server.md) | [JDBC Driver for SQL Server](jdbc/microsoft-jdbc-driver-for-sql-server.md) | [SQL Server용 OLE DB 드라이버](oledb/oledb-driver-for-sql-server.md) |
| :-- | :-- | :-- | :-- | :-- |
| [Always Encrypted](../relational-databases/security/encryption/always-encrypted-database-engine.md) | [예](odbc/using-always-encrypted-with-the-odbc-driver.md) | [예](odbc/using-always-encrypted-with-the-odbc-driver.md) | [예](jdbc/using-always-encrypted-with-the-jdbc-driver.md) |
| [보안 enclave를 사용한 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md) | [예](odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves) | [예](odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves) | [예](jdbc/using-always-encrypted-with-the-jdbc-driver.md) | |
| [Azure Active Directory 액세스 토큰 인증](/azure/active-directory/develop/access-tokens) | [예](odbc/using-azure-active-directory.md#authenticating-with-an-access-token) | [예](odbc/using-azure-active-directory.md#authenticating-with-an-access-token) | [예](jdbc/connecting-using-azure-active-directory-authentication.md#connecting-using-access-token) | [예](oledb/features/using-azure-active-directory.md) |
| [Azure Active Directory 암호 인증](/azure/sql-database/sql-database-aad-authentication) |  [예](odbc/using-azure-active-directory.md) | [예](odbc/using-azure-active-directory.md) | [예](jdbc/connecting-using-azure-active-directory-authentication.md) | [예](oledb/features/using-azure-active-directory.md) |
| [Azure Active Directory 통합 인증](/azure/sql-database/sql-database-aad-authentication) | [예](odbc/using-azure-active-directory.md) | [예](odbc/using-azure-active-directory.md) | [예](jdbc/connecting-using-azure-active-directory-authentication.md) | [예](oledb/features/using-azure-active-directory.md) |
| [Azure Active Directory 대화형(MFA) 인증](/azure/sql-database/sql-database-aad-authentication) | [예](odbc/using-azure-active-directory.md) | | | [예](oledb/features/using-azure-active-directory.md) |
| [Azure Active Directory 관리 ID 인증](/azure/active-directory/managed-identities-azure-resources/overview) | [예](odbc/using-azure-active-directory.md) | [예](odbc/using-azure-active-directory.md) | [예](jdbc/connecting-using-azure-active-directory-authentication.md) | [예](oledb/features/using-azure-active-directory.md) |
| [Azure Active Directory 서비스 사용자 인증](/azure/active-directory/develop/app-objects-and-service-principals) | | | | |
| [Windows 통합 인증](/windows-server/security/windows-authentication/windows-authentication-overview) | 예 | [예](odbc/linux-mac/using-integrated-authentication.md) | [예](jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) | 예 |
| [대량 복사](../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) | [예](../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md) | [예](../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md) | [예](jdbc/using-bulk-copy-with-the-jdbc-driver.md) | [예](oledb/features/performing-bulk-copy-operations.md) |
| [데이터 검색 및 분류 메타데이터](../relational-databases/security/sql-data-discovery-and-classification.md) | [예](odbc/data-classification.md) | [예](odbc/data-classification.md) | [예](jdbc/data-discovery-classification-sample.md) | |
| [MARS(Multiple Active Result Sets)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [예](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [예](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | | [예](oledb/features/using-multiple-active-result-sets-mars.md) |
| [공간 데이터 형식](../relational-databases/spatial/spatial-data-sql-server.md) | | | [예](jdbc/use-spatial-datatypes.md) | |
| [TVP(테이블 반환 매개 변수)](../relational-databases/tables/use-table-valued-parameters-database-engine.md) | [예](../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md) | [예](../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md) | [예](jdbc/using-table-valued-parameters.md) | [예](oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md) |
| [MultiSubnetFailover](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [예](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [예](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [예](jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md) | [예](oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) |
| [투명 네트워크 IP 확인](odbc/using-transparent-network-ip-resolution.md) | [예](odbc/using-transparent-network-ip-resolution.md) | [예](odbc/using-transparent-network-ip-resolution.md) | [예](jdbc/setting-the-connection-properties.md) | [예](oledb/features/using-transparent-network-ip-resolution.md) |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

| <a id="table3"></a>기능 | [Windows 기반 Drivers for PHP for SQL Server](php/microsoft-php-driver-for-sql-server.md)<sup>[1](#note1)</sup> | [Linux 및 macOS 기반 Drivers for PHP for SQL Server](php/microsoft-php-driver-for-sql-server.md)<sup>[1](#note1)</sup> | [Tedious(Node.js)](node-js/node-js-driver-for-sql-server.md) | [pyODBC(Python)](python/pyodbc/python-sql-driver-pyodbc.md)<sup>[1](#note1)</sup> |
| :-- | :-- | :-- | :-- | :-- |
| [Always Encrypted](../relational-databases/security/encryption/always-encrypted-database-engine.md) | [예](php/using-always-encrypted-php-drivers.md) | [예](php/using-always-encrypted-php-drivers.md) | | 예 |
| [보안 enclave를 사용한 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md) | [예](php/always-encrypted-secure-enclaves.md) | [예](php/always-encrypted-secure-enclaves.md) | | 예 |
| [Azure Active Directory 액세스 토큰 인증](/azure/active-directory/develop/access-tokens) | [예](php/azure-active-directory.md) | [예](php/azure-active-directory.md) | [예](https://tediousjs.github.io/tedious/api-connection.html#function_newConnection) | 예 |
| [Azure Active Directory 암호 인증](/azure/sql-database/sql-database-aad-authentication) | [예](php/azure-active-directory.md) | [예](php/azure-active-directory.md) | [예](https://tediousjs.github.io/tedious/api-connection.html#function_newConnection) | 예 |
| [Azure Active Directory 통합 인증](/azure/sql-database/sql-database-aad-authentication) | [예](php/azure-active-directory.md) | [예](php/azure-active-directory.md) | | 예 |
| [Azure Active Directory 대화형(MFA) 인증](/azure/sql-database/sql-database-aad-authentication) | | | | 예<sup>[2](#note2)</sup> |
| [Azure Active Directory 관리 ID 인증](/azure/active-directory/managed-identities-azure-resources/overview) | [예](php/azure-active-directory.md) | [예](php/azure-active-directory.md) | [예](https://tediousjs.github.io/tedious/api-connection.html#function_newConnection) | 예 |
| [Azure Active Directory 서비스 사용자 인증](/azure/active-directory/develop/app-objects-and-service-principals) | | | | |
| [Windows 통합 인증](/windows-server/security/windows-authentication/windows-authentication-overview) | [예](php/how-to-connect-using-windows-authentication.md) | [예](odbc/linux-mac/using-integrated-authentication.md) | | 예 |
| [대량 복사](../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) | | | [예](https://tediousjs.github.io/tedious/bulk-load.html) | |
| [데이터 검색 및 분류 메타데이터](../relational-databases/security/sql-data-discovery-and-classification.md) | yes | 예 | | |
| [MARS(Multiple Active Result Sets)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [예](php/how-to-disable-multiple-active-resultsets-mars.md) | [예](php/how-to-disable-multiple-active-resultsets-mars.md) | | 예 |
| [공간 데이터 형식](../relational-databases/spatial/spatial-data-sql-server.md) | | | | |
| [TVP(테이블 반환 매개 변수)](../relational-databases/tables/use-table-valued-parameters-database-engine.md) | | | [예](https://tediousjs.github.io/tedious/parameters.html) | 예 |
| [MultiSubnetFailover](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [예](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | [예](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | | [예](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) |
| [투명 네트워크 IP 확인](odbc/using-transparent-network-ip-resolution.md) | [예](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | [예](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | | [예](odbc/using-transparent-network-ip-resolution.md) |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<a id="note1"></a><sup>1</sup> 이러한 드라이버는 Microsoft ODBC Driver for SQL Server에 의존하므로 기능을 지원하는 드라이버 버전도 사용해야 합니다.

<a id="note2"></a><sup>2</sup> Windows에서만 지원됩니다.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
