---
title: 반환 코드 (Native Client OLE DB 공급자)
description: 일반적으로 발생 하는 DB_S_ERRORSOCCURRED HRESULT 값을 포함 하 여 SQL Server Native Client OLE DB에 대해 지원 되는 반환 코드에 대해 알아봅니다.
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 64111973f8e1c753a3d342c395d2f457ad1b3401
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97433829"
---
# <a name="return-codes-native-client-ole-db-provider"></a>반환 코드 (Native Client OLE DB 공급자)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  아주 간단히 말해 멤버 함수는 성공하거나 실패하거나 둘 중 하나입니다. 그러나 좀 더 정확하게 말하면 함수가 성공하더라도 이러한 성공이 애플리케이션 개발자가 의도한 것이 아닐 수 있습니다.  
  
 OLE DB 반환 코드에 대한 자세한 내용은 [반환 코드(OLE DB)](/previous-versions/windows/desktop/ms725451(v=vs.85))를 참조하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자 멤버 함수가 S_OK를 반환할 때 함수가 성공 했습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자 멤버 함수가 S_OK를 반환 하지 않는 경우 OLE/COM HRESULT-압축 풀기 실패 및 IS_ERROR 매크로는 함수의 전반적인 성공 또는 실패를 확인할 수 있습니다.  
  
 FAILED 또는 IS_ERROR에서 TRUE를 반환 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자는 멤버 함수를 실행 하지 못했음을 보장 합니다. FAILED 또는 IS_ERROR가 FALSE를 반환 하 고 HRESULT가 S_OK와 같지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자는 함수가 정상적으로 성공 했음을 보장 합니다. 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 오류 인터페이스에서이 "정보를 사용 하 여 성공 했습니다."에 대 한 자세한 정보를 검색할 수 있습니다. 또한 함수가 오류를 명확 하 게 실패 한 경우 (실패 한 매크로는 TRUE를 반환 함) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 오류 인터페이스에서 확장 오류 정보를 사용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자는 일반적으로 "success with information" HRESULT를 반환 DB_S_ERRORSOCCURRED 발생 합니다. 일반적으로 DB_S_ERRORSOCCURRED를 반환하는 멤버 함수는 소비자에게 상태 값을 전달하는 하나 이상의 매개 변수를 정의합니다. status-value 매개 변수에 반환되는 정보 외에 다른 오류 정보가 제공되지 않을 수 있으므로 소비자는 제공되는 경우에 상태 값을 검색하도록 애플리케이션 논리를 구현해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자 멤버 함수는 S_FALSE 성공 코드를 반환 하지 않습니다. 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 멤버 함수는 항상 성공을 나타내는 S_OK를 반환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Errors](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
