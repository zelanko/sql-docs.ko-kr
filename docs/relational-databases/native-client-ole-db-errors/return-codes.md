---
title: "반환 코드 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-errors
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- OLE DB error handling, return codes
- SQL Server Native Client OLE DB provider, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
ms.assetid: 7f7457e9-fce4-400c-82e5-ee02e9e811c6
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 130c0faf625626d2da0376b5b4d47795573d10c1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="return-codes"></a>반환 코드
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  아주 간단히 말해 멤버 함수는 성공하거나 실패하거나 둘 중 하나입니다. 그러나 좀 더 정확하게 말하면 함수가 성공하더라도 이러한 성공이 응용 프로그램 개발자가 의도한 것이 아닐 수 있습니다.  
  
 OLE DB 반환 코드에 대 한 자세한 내용은 참조 [반환 코드 (OLE DB)](http://go.microsoft.com/fwlink/?LinkId=101631)합니다.  
  
 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 멤버 함수가 S_OK를 성공 함수를 반환 합니다.  
  
 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 멤버 함수가 S_OK를 반환 하지 않습니다, 전반적인 성공 또는 실패는 함수의 OLE/COM hresult-unpacking FAILED 및 IS_ERROR 매크로 확인할 수 있습니다.  
  
 FAILED 또는 is_error가 TRUE를 반환 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자는 멤버 함수 실행이 실패 했음을 확인할 합니다. FAILED 또는 is_error가 FALSE이 고 HRESULT 반환 하는 경우 s_ok이 고, 같지 않음는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자가 어떤 의미에서 함수 성공 것을 보장 합니다. 소비자는이 "성공 시 정보와 함께"에서 반환 하는 세부 정보를 검색할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 오류 인터페이스입니다. 또한 (의 FAILED 매크로가 TRUE를 반환한)에 함수 명확 하 게 실패 하는 경우 확장된 오류 정보는에서 사용할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 오류 인터페이스입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자 소비자는 정보로 DB_S_ERRORSOCCURRED "성공" HRESULT 반환 되는 일반적으로 발생 합니다. 일반적으로 DB_S_ERRORSOCCURRED를 반환하는 멤버 함수는 소비자에게 상태 값을 전달하는 하나 이상의 매개 변수를 정의합니다. status-value 매개 변수에 반환되는 정보 외에 다른 오류 정보가 제공되지 않을 수 있으므로 소비자는 제공되는 경우에 상태 값을 검색하도록 응용 프로그램 논리를 구현해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 멤버 함수는 성공 코드 S_FALSE를 반환 하지 않습니다. 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 멤버 함수에는 항상 성공을 표시 하기 위해 S_OK를 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [오류](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
