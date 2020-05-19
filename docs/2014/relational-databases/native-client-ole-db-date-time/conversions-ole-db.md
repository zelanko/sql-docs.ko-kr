---
title: 바인딩 및 변환(OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB]
- bindings [OLE DB]
- OLE DB, bindings and conversions
ms.assetid: c187df58-a8c8-4c74-a76f-663abbc5f0c1
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d920fef68adaa63059970a49c9473d75eeabfd30
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705053"
---
# <a name="bindings-and-conversions-ole-db"></a>바인딩 및 변환(OLE DB)
  이 섹션에서는 `datetime` 값과 `datetimeoffset` 값 사이의 변환 방법에 대해 설명합니다. 이 섹션에 설명된 변환은 OLE DB에서 이미 제공하거나 OLE DB의 일관된 확장입니다.  
  
 OLE DB에서 날짜와 시간에 대한 리터럴 및 문자열 형식은 일반적으로 ISO를 따르며 클라이언트 로캘에 종속되지 않습니다. 한 가지 예외는 OLE Automation이 표준인 DBTYPE_DATE이지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에서는 클라이언트와의 사이에 데이터가 전송되는 경우에만 형식을 변환하기 때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client가 애플리케이션에 의해 강제로 DBTYPE_DATE와 문자열 형식 사이를 변환하는 경우는 없습니다. 이러한 경우를 제외하면 문자열에는 다음과 같은 형식이 사용됩니다. 여기서 대괄호 안의 텍스트는 선택적 요소를 나타냅니다.  
  
-   `datetime` 및 `datetimeoffset` 문자열의 형식  
  
     *yyyy* - *mm* - *dd*[ *hh*:*mm*:*ss*[.* 9999999*] [?? *hh*:*mm*]]  
  
-   `time` 문자열의 형식  
  
     *hh*:*mm*:*ss*[.*9999999*]  
  
-   `date` 문자열의 형식  
  
     *yyyy*-*mm*-*dd*  
  
> [!NOTE]  
>  이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client와 SQLOLEDB에서는 OLE 변환을 구현했으며 이 경우 표준 변환은 실패했습니다. 그 결과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 10.0 이상에서 수행하는 변환 중 일부는 OLE DB 사양과 다릅니다.  
  
 문자열에서 변환을 시작하면 공백 및 필드 너비를 보다 융통성 있게 사용할 수 있습니다. 자세한 내용은 [OLE DB 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](data-type-support-for-ole-db-date-and-time-improvements.md)의 "데이터 형식: 문자열 및 리터럴" 섹션을 참조 하세요.  
  
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
 [클라이언트에서 서버로 수행되는 변환](conversions-performed-from-client-to-server.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB를 사용하여 작성된 클라이언트 애플리케이션과 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 간에 수행되는 날짜/시간 변환에 대해 설명합니다.  
  
 [서버에서 클라이언트로 수행되는 변환](conversions-performed-from-server-to-client.md)  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB를 사용하여 작성된 클라이언트 애플리케이션 간에 수행되는 날짜/시간 변환에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [날짜 및 시간 기능 향상&#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
