---
title: 코드를 반환 합니다. | Microsoft Docs
description: 반환 코드
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
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
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 7bb86d9e9c43b6d8c73f8018e80eebd5a0a54f5e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66786063"
---
# <a name="return-codes"></a>반환 코드
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  아주 간단히 말해 멤버 함수는 성공하거나 실패하거나 둘 중 하나입니다. 그러나 좀 더 정확하게 말하면 함수가 성공하더라도 이러한 성공이 응용 프로그램 개발자가 의도한 것이 아닐 수 있습니다.  
  
 OLE DB 반환 코드에 대한 자세한 내용은 [반환 코드(OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631)를 참조하십시오.  
  
 S_OK를 반환 하는 OLE DB 드라이버는 SQL Server 멤버 함수, 함수 성공 했습니다.  
  
 SQL Server용 OLE DB 드라이버 멤버 함수가 S_OK를 반환하지 않으면 OLE/COM HRESULT-unpacking FAILED 및 IS_ERROR 매크로를 통해 함수의 전반적인 성공 또는 실패를 확인할 수 있습니다.  
  
 FAILED 또는 IS_ERROR가 TRUE를 반환하면 SQL Server용 OLE DB 드라이버 소비자는 멤버 함수 실행이 실패했음을 확인할 수 있습니다. FAILED 또는 IS_ERROR가 반환 하는 경우 FALSE이 고 HRESULT와 같지 않은 S_OK는 OLE DB Driver for SQL Server 소비자가 어떤 의미에서 성공 하는 함수를 보장 합니다. 소비자는 SQL Server용 OLE DB 드라이버 오류 인터페이스에서 이러한 “정보를 포함한 성공 메시지” 반환에 대한 자세한 정보를 검색할 수 있습니다. 또한 함수가 확실히 실패한 경우(FAILED 매크로가 TRUE를 반환한 경우)에도 SQL Server용 OLE DB 드라이버 오류 인터페이스에서 확장 오류 정보를 얻을 수 있습니다.  
  
 OLE DB Driver for SQL Server 소비자가 정보를 사용 하 여 DB_S_ERRORSOCCURRED "성공" HRESULT 반환을 일반적으로 발생 합니다. 일반적으로 DB_S_ERRORSOCCURRED를 반환하는 멤버 함수는 소비자에게 상태 값을 전달하는 하나 이상의 매개 변수를 정의합니다. status-value 매개 변수에 반환되는 정보 외에 다른 오류 정보가 제공되지 않을 수 있으므로 소비자는 제공되는 경우에 상태 값을 검색하도록 애플리케이션 논리를 구현해야 합니다.  
  
 OLE DB Driver for SQL Server 멤버 함수는 성공 코드 S_FALSE를 반환 하지 않습니다. 모든 OLE DB Driver for SQL Server 멤버 함수는 항상 성공을 표시 하기 위해 S_OK를 반환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [오류](../../oledb/ole-db-errors/errors.md)  
  
  
