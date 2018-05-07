---
title: 반환 코드 | Microsoft Docs
description: 반환 코드
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB error handling, return codes
- OLE DB Driver for SQL Server, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 18564da5e47a6b28b92841163847bfd0b8a28aa0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="return-codes"></a>반환 코드
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  아주 간단히 말해 멤버 함수는 성공하거나 실패하거나 둘 중 하나입니다. 그러나 좀 더 정확하게 말하면 함수가 성공하더라도 이러한 성공이 응용 프로그램 개발자가 의도한 것이 아닐 수 있습니다.  
  
 OLE DB 반환 코드에 대 한 자세한 내용은 참조 [반환 코드 (OLE DB)](http://go.microsoft.com/fwlink/?LinkId=101631)합니다.  
  
 OLE DB Driver for SQL Server 멤버 함수가 S_OK를 반환 하는 경우 함수는 성공 했습니다.  
  
 OLE DB 드라이버는 SQL Server 멤버 함수가 S_OK를 반환 하지 않습니다, 전반적인 성공 또는 실패는 함수의 OLE/COM hresult-unpacking FAILED 및 IS_ERROR 매크로 확인할 수 있습니다.  
  
 FAILED 또는 is_error가 TRUE를 반환 멤버 함수 실행이 실패는 OLE DB Driver for SQL Server 소비자가 보장 됩니다. FAILED 또는 is_error가 반환 하는 경우 FALSE이 고 HRESULT와 같지 않습니다 s_ok이 고는 OLE DB Driver for SQL Server 소비자는 함수가 어떤 의미에서 성공한 보장 됩니다. 소비자는 OLE DB Driver for SQL Server 오류 인터페이스에서에서이 "정보를 포함 한 성공" 반환에 대 한 자세한 정보를 검색할 수 있습니다. 또한 (의 FAILED 매크로가 TRUE를 반환한)에 함수 명확 하 게 실패 하는 경우 확장된 오류 정보는 OLE DB 드라이버에서 SQL Server 오류 인터페이스에서 사용할 수 있습니다.  
  
 OLE DB Driver for SQL Server 소비자가 정보와 함께 DB_S_ERRORSOCCURRED "성공" HRESULT 반환을 일반적으로 발생 합니다. 일반적으로 DB_S_ERRORSOCCURRED를 반환하는 멤버 함수는 소비자에게 상태 값을 전달하는 하나 이상의 매개 변수를 정의합니다. 오류 정보가 소비자가 사용할 수 있을 때 상태 값을 검색 하도록 응용 프로그램 논리를 구현 해야 하므로 상태 값 매개 변수, 반환 되는 다른 소비자에 게 사용할 수 있습니다.  
  
 OLE DB 드라이버에서 SQL Server 멤버 함수는 성공 코드 S_FALSE를 반환 하지 않습니다. 모든 OLE DB Driver for SQL Server 멤버 함수는 항상 성공을 표시 하기 위해 S_OK를 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [오류](../../oledb/ole-db-errors/errors.md)  
  
  
