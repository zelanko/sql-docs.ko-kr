---
title: 유니버설 데이터 링크 (UDL) 구성 | Microsoft Docs
description: SQL Server 용 Microsoft OLE DB 드라이버를 사용 하 여 유니버설 데이터 링크 (UDL) 구성
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: e198f561fd4f6bcec390ef8632c1cdc96f2810d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62854663"
---
# <a name="universal-data-link-udl-configuration"></a>UDL(유니버설 데이터 링크) 구성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="connection-tab"></a>연결 탭
연결 탭을 사용 하 여 SQL Server 용 Microsoft OLE DB 드라이버를 사용 하 여 데이터에 연결 하는 방법을 지정 합니다.

![OLE DB 데이터 연결 페이지-연결 탭의 스크린샷](../media/data-link-pages-connection-tab.png)

이 연결 탭은 공급자별 옵션이며 Microsoft OLE DB Driver for SQL Server에 필요한 연결 속성만 표시합니다.

|옵션|설명|
|---   |---        |
|서버 이름 선택 또는 입력|드롭다운 목록에서 서버 이름을 선택하거나 액세스할 데이터베이스가 있는 서버의 위치를 입력합니다. 서버에서 데이터베이스를 선택하는 것은 별개의 동작입니다. “새로 고침”을 클릭하여 목록을 업데이트합니다.
|서버에 로그인 하는 정보를 입력 합니다.|이 드롭다운 목록에서 다음 인증 옵션을 선택할 수 있습니다. <ul><li>`Windows Authentication:` 현재 로그인 한 사용자의 Windows 계정 자격 증명을 사용 하 여 SQL Server에 인증 합니다.</li><li>`SQL Server Authentication:` SQL server 로그인 ID 및 암호를 사용 하 여 인증 합니다.</li><li>`Active Directory - Integrated:` 현재 로그인 한 사용자의 Windows 계정 자격 증명을 사용 하 여 통합된 인증입니다.</li><li>`Active Directory - Password:` Active Directory 인증 로그인 ID 및 암호를 사용 합니다.</li></ul>|
|서버 SPN|트러스트된 연결을 사용하면 서버에 대한 SPN(서비스 사용자 이름)을 지정할 수 있습니다.|
|사용자 이름|데이터 원본에 로그인 할 때 인증에 사용할 사용자 ID를 입력 합니다.|
|암호|데이터 원본에 로그인 할 때 인증에 사용할 암호를 입력 합니다.|
|빈 암호|옵션을 선택 하면 연결 문자열에서 빈 암호를 사용 하도록 지정된 된 공급자를 사용 하도록 설정 합니다.|
|암호 저장 허용|이 옵션을 선택 하면 암호를 연결 문자열을 사용 하 여 저장 합니다. 암호가 연결 문자열에 포함되는지 여부는 호출 애플리케이션의 기능에 따라 달라집니다. <br/><br/>**참고:** 저장되면 암호는 마스크되거나 암호화되지 않고 반환 및 저장됩니다.|
|데이터에 대하여 강력한 암호화 사용|옵션을 선택 하면 연결을 통해 전달 되는 데이터가 암호화 됩니다.|
|서버 인증서 신뢰|옵션을 선택 하면 서버 인증서의 유효성이 검사 됩니다. 서버 인증서 서버의 올바른 호스트 이름이 있고 신뢰할 수 있는 인증 기관에서 발급 합니다.|
|데이터베이스 선택|선택 하거나 액세스 하려면 데이터베이스 이름을 입력 합니다.|
|데이터베이스 파일을 데이터베이스 이름으로 연결|연결할 수 있는 데이터베이스에 대한 주 파일의 이름을 지정합니다. 이 데이터베이스는 데이터 원본에 대한 기본 데이터베이스로 연결되어 사용됩니다. 이 섹션에서 첫 번째 텍스트 상자에 연결 된 데이터베이스 파일에 사용할 데이터베이스 이름을 입력 합니다.<br/><br/>레이블이 지정 된 텍스트 상자에서 연결할 데이터베이스 파일의 전체 경로 입력 `Using the filename`를 클릭 또는 `...` 클릭 하 여 데이터베이스 파일에 대 한 검색 합니다.|
|암호 변경|SQL Server 암호 변경 대화 상자를 표시 합니다. |
|연결 테스트|지정된 된 데이터 원본에 대 한 연결을 시도 하려면 클릭 합니다. 연결이 실패할 경우 설정이 올바른지 확인하십시오. 예를 들어 맞춤법 오류 및 대/소문자 구분으로 인해 연결이 실패할 수 있습니다.|

## <a name="advanced-tab"></a>고급 탭
보기 및 추가 초기화 속성을 설정 하려면 [고급] 탭을 사용 합니다.

![OLE DB 데이터 연결 페이지-고급 탭의 스크린샷](../media/data-link-pages-advanced-tab.png)

|옵션|설명|
|---   |---        |
| Connect timeout | Microsoft OLE DB Driver for SQL Server가 초기화가 완료 될 때까지 대기 시간 (초)의 양을 지정 합니다. 초기화가 제한 시간을 초과하면 오류가 반환되며 연결이 만들어지지 않습니다.|


> [!NOTE]  
>  보다 일반적인 데이터 연결 연결 정보에 대 한 참조를 [데이터 링크 API 개요](https://go.microsoft.com/fwlink/?linkid=2067432)합니다.

## <a name="next-steps"></a>다음 단계
- [Azure Active Directory에 인증](../features/using-azure-active-directory.md) OLE DB 드라이버를 사용 합니다.

- [인증 자격 증명에 대 한 사용자에 게](../help-topics/sql-server-login-dialog.md) OLE DB 드라이버를 사용 합니다.