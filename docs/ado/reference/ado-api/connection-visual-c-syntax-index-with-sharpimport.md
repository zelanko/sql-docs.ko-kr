---
description: Connection (#import를 사용 하는 Visual C++ 구문 인덱스)
title: Connection (#import를 사용 하는 Visual C++ 구문 인덱스) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- 'Connection collection [ADO], Visual C++ syntax index with #import'
ms.assetid: 03f47eda-840d-4cab-83d9-ccddd873f342
author: rothja
ms.author: jroth
ms.openlocfilehash: 9ee7e847b9e57b10520bfe8ac77af638214b5126
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444495"
---
# <a name="connection-visual-c-syntax-index-with-import"></a>Connection (#import를 사용 하는 Visual C++ 구문 인덱스)
## <a name="methods"></a>메서드  
  
```  
HRESULT Cancel( );  
HRESULT Close( );  
_RecordsetPtr Execute( _bstr_t CommandText, VARIANT *  
    RecordsAffected,     long Options );  
long BeginTrans( );  
HRESULT CommitTrans( );  
HRESULT RollbackTrans( );  
HRESULT Open( _bstr_t ConnectionString, _bstr_t UserID,  
    _bstr_t Password,     long Options );  
_RecordsetPtr OpenSchema( enum SchemaEnum Schema, const  
    _variant_t &     Restrictions = vtMissing, const _variant_t &   
    SchemaID = vtMissing );  
```  
  
## <a name="properties"></a>속성  
  
```  
_bstr_t GetConnectionString( );  
void PutConnectionString( _bstr_t pbstr );  
__declspec(property(get=GetConnectionString,put=PutConnectionString))  
    _bstr_t ConnectionString;  
long GetCommandTimeout( );  
void PutCommandTimeout( long plTimeout );  
__declspec(property(get=GetCommandTimeout,put=PutCommandTimeout)) long  
    CommandTimeout;  
long GetConnectionTimeout( );  
void PutConnectionTimeout( long plTimeout );  
__declspec(property(get=GetConnectionTimeout,put=PutConnectionTimeout))  
    long ConnectionTimeout;  
_bstr_t GetVersion( );  
__declspec(property(get=GetVersion)) _bstr_t Version;  
ErrorsPtr GetErrors( );  
__declspec(property(get=GetErrors)) ErrorsPtr Errors;  
_bstr_t GetDefaultDatabase( );  
void PutDefaultDatabase( _bstr_t pbstr );  
__declspec(property(get=GetDefaultDatabase,put=PutDefaultDatabase))  
    _bstr_t DefaultDatabase;  
enum IsolationLevelEnum GetIsolationLevel( );  
void PutIsolationLevel( enum IsolationLevelEnum Level );  
__declspec(property(get=GetIsolationLevel,put=PutIsolationLevel)) enum  
    IsolationLevelEnum IsolationLevel;  
long GetAttributes( );  
void PutAttributes( long plAttr );  
__declspec(property(get=GetAttributes,put=PutAttributes)) long  
    Attributes;  
enum CursorLocationEnum GetCursorLocation( );  
void PutCursorLocation( enum CursorLocationEnum plCursorLoc );  
__declspec(property(get=GetCursorLocation,put=PutCursorLocation)) enum  
    CursorLocationEnum CursorLocation;  
enum ConnectModeEnum GetMode( );  
void PutMode( enum ConnectModeEnum plMode );  
__declspec(property(get=GetMode,put=PutMode)) enum ConnectModeEnum  
    Mode;  
_bstr_t GetProvider( );  
void PutProvider( _bstr_t pbstr );  
__declspec(property(get=GetProvider,put=PutProvider)) _bstr_t  
    Provider;  
long GetState( );  
__declspec(property(get=GetState)) long State;  
```  
  
## <a name="see-also"></a>참고 항목  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
