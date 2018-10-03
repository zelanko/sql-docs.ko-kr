---
title: 바인딩 및 변환 (OLE DB) | Microsoft Docs
description: 바인딩 및 변환 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB]
- bindings [OLE DB]
- OLE DB, bindings and conversions
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 9eca16e0908bac5134d459414cbd43ee19a4665a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724961"
---
# <a name="conversions-ole-db"></a>변환(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  이 섹션에서는 간에 변환 하는 방법 설명 **날짜/시간** 하 고 **datetimeoffset** 값입니다. 이 섹션에 설명된 변환은 OLE DB에서 이미 제공하거나 OLE DB의 일관된 확장입니다.  
  
 OLE DB에서 날짜와 시간에 대한 리터럴 및 문자열 형식은 일반적으로 ISO를 따르며 클라이언트 로캘에 종속되지 않습니다. 한 가지 예외는 OLE Automation이 표준인 DBTYPE_DATE이지만 그러나 OLE DB Driver for SQL Server 데이터와 클라이언트에서 전송 될 때 형식 간의 변환, 이므로 OLE DB Driver for SQL Server DBTYPE_DATE와 문자열 형식 간의 변환 하도록 응용 프로그램에 대 한 방법은 없습니다. 이러한 경우를 제외하면 문자열에는 다음과 같은 형식이 사용됩니다. 여기서 대괄호 안의 텍스트는 선택적 요소를 나타냅니다.  
  
-   형식은 **날짜/시간** 하 고 **datetimeoffset** 문자열:  
  
     *yyyy*-*mm*-*dd*[ *hh*:*mm*:*ss*[. *9999999*] [에서 *hh*:*mm*]]  
  
-   **시간** 문자열의 형식은 다음과 같습니다.  
  
     *hh*:*mm*:*ss*[.*9999999*]  
  
-   형식은 **날짜** 문자열:  
  
     *yyyy*-*mm*-*dd*  
  
> [!NOTE]  
>  이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 SQLOLEDB에서는 OLE 변환을 구현했으며 이 경우 표준 변환은 실패했습니다. OLE DB Driver for SQL Server와 같은 동작을 따릅니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client입니다. 결과적으로, SQL Server 용 OLE DB 드라이버에서 수행 되는 일부 변환에서 OLE DB 사양과 다릅니다.  
  
 문자열에서 변환을 시작하면 공백 및 필드 너비를 보다 융통성 있게 사용할 수 있습니다. 자세한 내용은의 "데이터 형식:: 문자열 및 리터럴" 섹션을 참조 하세요 [OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)합니다.  
  
 일반적인 변환 규칙은 다음과 같습니다.  
  
-   문자열을 날짜/시간 형식으로 변환하면 문자열이 먼저 ISO 리터럴로 구문 분석됩니다. 구문 분석이 실패하면 문자열은 시간 구성 요소가 있는 OLE 날짜 리터럴로 구문 분석됩니다.  
  
-   시간 구성 요소가 없지만 받는 사람이 시간을 저장할 수 있는 경우 시간이 0으로 설정됩니다. 날짜 구성 요소가 없지만 받는 사람이 날짜를 저장할 수 있는 경우, ISO 변환을 사용하면 날짜가 현재 날짜로 설정되고 OLE 변환을 사용하면 날짜가 1899-12-30으로 설정됩니다.  
  
-   클라이언트에서 사용하는 데이터 형식에는 표준 시간대가 없지만 서버에서 표준 시간대를 저장할 수 있는 경우 클라이언트의 데이터는 클라이언트 표준 시간대를 기준으로 하는 것으로 간주합니다.  
  
-   서버에는 표준 시간대가 없지만 클라이언트에 표준 시간대 정보가 있는 경우 UTC 표준 시간대가 사용됩니다. 이는 서버 동작과는 다릅니다.  
  
-   시간 구성 요소가 있지만 받는 사람이 시간을 저장할 수 없는 경우 시간 구성 요소는 무시됩니다.  
  
-   날짜 구성 요소가 있지만 받는 사람이 날짜를 저장할 수 없는 경우 날짜 구성 요소는 무시됩니다.  
  
-   클라이언트에서 서버로 변환할 때 초 또는 소수 자릿수 초가 잘리는 경우 DB_E_ERRORSOCCURRED가 반환되고 DBSTATUS_E_DATAOVERFLOW 상태가 설정됩니다.  
  
-   서버에서 클라이언트로 변환할 때 초 또는 소수 자릿수 초가 잘리는 경우 DBSTATUS_S_TRUNCATED가 설정됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [클라이언트에서 서버로 수행되는 변환](../../oledb/ole-db-date-time/conversions-performed-from-client-to-server.md)  
 SQL Server 용 OLE DB 드라이버를 사용하여 작성된 클라이언트 응용 프로그램과 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 이상 간에 수행되는 날짜/시간 변환에 대해 설명합니다.  
  
 [서버에서 클라이언트로 수행되는 변환](../../oledb/ole-db-date-time/conversions-performed-from-server-to-client.md)  
 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 이상과 SQL Server 용 OLE DB 드라이버를 사용하여 작성된 클라이언트 응용 프로그램 간에 수행되는 날짜/시간 변환에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [날짜 및 시간 기능 향상&#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
