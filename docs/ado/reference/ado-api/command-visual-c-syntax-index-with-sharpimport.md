---
description: Command (#import를 사용 하는 Visual C++ 구문 인덱스)
title: Command (#import를 사용 하는 Visual C++ 구문 인덱스) | Microsoft Docs
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
- 'Command collection [ADO], Visual C++ syntax index with #import'
ms.assetid: ccb6ffbc-7303-4124-8a0c-f6356f2c82d9
author: rothja
ms.author: jroth
ms.openlocfilehash: 02ba483a38f554455d1b30546a9308aeec3921ed
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776132"
---
# <a name="command-visual-c-syntax-index-with-import"></a>Command (#import를 사용 하는 Visual C++ 구문 인덱스)
## <a name="methods"></a>메서드  
  
```  
HRESULT Cancel( );  
_RecordsetPtr Execute( VARIANT * RecordsAffected, VARIANT * Parameters, long Options );  
_ParameterPtr CreateParameter( _bstr_t Name, enum DataTypeEnum Type, enum ParameterDirectionEnum Direction, long Size, const _variant_t & Value = vtMissing );  
```  
  
## <a name="properties"></a>속성  
  
```  
_ConnectionPtr GetActiveConnection( );  
void PutRefActiveConnection( struct _Connection * ppvObject );  
void PutActiveConnection( const _variant_t & ppvObject ); __declspec(property(get=GetActiveConnection,put=PutRefActiveConnection)) _ConnectionPtr ActiveConnection;  
_bstr_t GetCommandText( );  
void PutCommandText( _bstr_t pbstr );  
__declspec(property(get=GetCommandText,put=PutCommandText)) _bstr_t  
    CommandText;  
long GetCommandTimeout( );  
void PutCommandTimeout( long pl );  
__declspec(property(get=GetCommandTimeout,put=PutCommandTimeout)) long CommandTimeout;  
void PutCommandType( enum CommandTypeEnum plCmdType );  
enum CommandTypeEnum GetCommandType( );  
__declspec(property(get=GetCommandType,put=PutCommandType)) enum CommandTypeEnum CommandType;  
VARIANT_BOOL GetPrepared( );  
void PutPrepared( VARIANT_BOOL pfPrepared );  
__declspec(property(get=GetPrepared,put=PutPrepared)) VARIANT_BOOL Prepared;  
ParametersPtr GetParameters( );  
__declspec(property(get=GetParameters)) ParametersPtr Parameters;  
_bstr_t GetName( );  
void PutName( _bstr_t pbstrName );  
__declspec(property(get=GetName,put=PutName)) _bstr_t Name;  
long GetState( );  
__declspec(property(get=GetState)) long State;  
```  
  
## <a name="see-also"></a>참고 항목  
 [명령 개체(ADO)](./command-object-ado.md)