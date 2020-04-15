---
title: 반환 코드 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 09056c9d4964ad10b2b25f63ef5991a1a7742cab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301033"
---
# <a name="return-codes"></a>반환 코드
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  아주 간단히 말해 멤버 함수는 성공하거나 실패하거나 둘 중 하나입니다. 그러나 좀 더 정확하게 말하면 함수가 성공하더라도 이러한 성공이 애플리케이션 개발자가 의도한 것이 아닐 수 있습니다.  
  
 OLE DB 반환 코드에 대한 자세한 내용은 [반환 코드(OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631)를 참조하십시오.  
  
 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자 함수가 S_OK 반환하면 함수가 성공했습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자 함수가 S_OK 반환하지 않으면 OLE/COM HRESULT 압축 풀기 실패 및 IS_ERROR 매크로가 함수의 전반적인 성공 또는 실패를 확인할 수 있습니다.  
  
 FAILED 또는 IS_ERROR TRUE를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환하는 경우 네이티브 클라이언트 OLE DB 공급자 소비자는 멤버 함수 실행이 실패했는지 보증합니다. FAILED 또는 IS_ERROR false를 반환하고 HRESULT가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] S_OK 같지 않은 경우 네이티브 클라이언트 OLE DB 공급자 소비자는 함수가 어떤 의미에서 성공했다는 것을 보장합니다. 소비자는 네이티브 클라이언트 OLE DB 공급자 오류 인터페이스에서 이 "정보 성공" 반환에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자세한 정보를 검색할 수 있습니다. 또한 함수가 명확하게 실패하는 경우(FAILED 매크로가 TRUE를 반환함) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자 오류 인터페이스에서 확장 된 오류 정보를 사용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]네이티브 클라이언트 OLE DB 공급자 소비자는 일반적으로 "정보와 성공" HRESULT 반환에 DB_S_ERRORSOCCURRED 발생 합니다. 일반적으로 DB_S_ERRORSOCCURRED를 반환하는 멤버 함수는 소비자에게 상태 값을 전달하는 하나 이상의 매개 변수를 정의합니다. status-value 매개 변수에 반환되는 정보 외에 다른 오류 정보가 제공되지 않을 수 있으므로 소비자는 제공되는 경우에 상태 값을 검색하도록 애플리케이션 논리를 구현해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자 멤버 함수는 성공 코드를 반환하지 S_FALSE. 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자 함수는 항상 성공을 나타내기 위해 S_OK 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [오류](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
