---
title: 대규모 데이터 가져오기 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버를 사용 하는 대규모 데이터 가져오기
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- DBPROP_ACCESSORDER property
- OLE DB Driver for SQL Server, BLOBs
- large data, OLE objects
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 603bbe774c115f9a5119f34bd1e9941549baf572
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773781"
---
# <a name="getting-large-data"></a>대규모 데이터 가져오기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  일반적으로 소비자는 SQL Server용 OLE DB 드라이버 저장소 개체를 만드는 코드를 **ISequentialStream** 인터페이스 포인터를 통해 참조되지 않는 데이터를 처리하는 다른 코드와 구분해야 합니다.  
  
 이 문서에서는 다음 함수와 함께 사용할 수 있는 기능에 대해 설명합니다.  
  
-   IRowset:GetData  
  
-   IRow::GetColumns  
  
-   ICommand::Execute  
  
 행 집합 속성 그룹의 DBPROP_ACCESSORDER 속성이 DBPROPVAL_AO_SEQUENTIAL 또는 DBPROPVAL_AO_SEQUENTIALSTORAGEOBJECTS 중 하나로 설정되어 있으면 소비자는 **GetNextRows** 메서드 호출에서 단일 데이터 행만 인출해야 합니다. BLOB 데이터가 버퍼링 되지 때문입니다. DBPROP_ACCESSORDER 값이 DBPROPVAL_AO_RANDOM으로 설정되어 있으면 소비자가 **GetNextRows**에서 여러 데이터 행을 인출할 수 있습니다.  
  
 OLE DB Driver for SQL Server에서 큰 데이터를 검색 하지 않습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이렇게 하려면 소비자가 요청할 때까지 합니다. 소비자는 모든 소규모 데이터를 하나의 접근자에 바인딩한 다음 필요에 따라 하나 이상의 임시 접근자를 사용하여 대규모 데이터 값을 검색해야 합니다.  
  
## <a name="example"></a>예제  
 이 예는 단일 열에서 대규모 데이터 값을 검색합니다.  
  
```  
HRESULT GetUnboundData  
    (  
    IRowset* pIRowset,  
    HROW hRow,  
    ULONG nCol,   
    BYTE* pUnboundData  
    )  
    {  
    UINT                cbRow = sizeof(IUnknown*) + sizeof(ULONG);  
    BYTE*               pRow = new BYTE[cbRow];  
  
    DBOBJECT            dbobject;  
  
    IAccessor*          pIAccessor = NULL;  
    HACCESSOR           haccessor;  
  
    DBBINDING           dbbinding;  
    ULONG               ulbindstatus;  
  
    ULONG               dwStatus;  
    ISequentialStream*  pISequentialStream;  
    ULONG               cbRead;  
  
    HRESULT             hr;  
  
    // Set up the DBOBJECT structure.  
    dbobject.dwFlags = STGM_READ;  
    dbobject.iid = IID_ISequentialStream;  
  
    // Create the DBBINDING, requesting a storage-object pointer from  
    // The OLE DB Driver for SQL Server.  
    dbbinding.iOrdinal = nCol;  
    dbbinding.obValue = 0;  
    dbbinding.obStatus = sizeof(IUnknown*);  
    dbbinding.obLength = 0;  
    dbbinding.pTypeInfo = NULL;  
    dbbinding.pObject = &dbobject;  
    dbbinding.pBindExt = NULL;  
    dbbinding.dwPart = DBPART_VALUE | DBPART_STATUS;  
    dbbinding.dwMemOwner = DBMEMOWNER_CLIENTOWNED;  
    dbbinding.eParamIO = DBPARAMIO_NOTPARAM;  
    dbbinding.cbMaxLen = 0;  
    dbbinding.dwFlags = 0;  
    dbbinding.wType = DBTYPE_IUNKNOWN;  
    dbbinding.bPrecision = 0;  
    dbbinding.bScale = 0;  
  
    if (FAILED(hr = pIRowset->  
        QueryInterface(IID_IAccessor, (void**) &pIAccessor)))  
        {  
        // Process QueryInterface failure.  
        return (hr);  
        }  
  
    // Create the accessor.  
    if (FAILED(hr = pIAccessor->CreateAccessor(DBACCESSOR_ROWDATA, 1,  
        &dbbinding, 0, &haccessor, &ulbindstatus)))  
        {  
        // Process error from CreateAccessor.  
        pIAccessor->Release();  
        return (hr);  
        }  
  
    // Read and process BLOCK_SIZE bytes at a time.  
    if (SUCCEEDED(hr = pIRowset->GetData(hRow, haccessor, pRow)))  
        {  
        dwStatus = *((ULONG*) (pRow + dbbinding.obStatus));  
  
        if (dwStatus == DBSTATUS_S_ISNULL)  
            {  
            // Process NULL data  
            }  
        else if (dwStatus == DBSTATUS_S_OK)  
            {  
            pISequentialStream = *((ISequentialStream**)   
                (pRow + dbbinding.obValue));  
  
            do  
                {  
                if (SUCCEEDED(hr =  
                    pISequentialStream->Read(pUnboundData,  
                    BLOCK_SIZE, &cbRead)))  
                    {  
                    pUnboundData += cbRead;  
                    }  
                }  
            while (SUCCEEDED(hr) && cbRead >= BLOCK_SIZE);  
  
            pISequentialStream->Release();  
            }  
        }  
    else  
        {  
        // Process error from GetData.  
        }  
  
    pIAccessor->ReleaseAccessor(haccessor, NULL);  
    pIAccessor->Release();  
    delete [] pRow;  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>참고 항목  
 [BLOB 및 OLE 개체](../../oledb/ole-db-blobs/blobs-and-ole-objects.md)   
 [큰 값 형식 사용](../../oledb/features/using-large-value-types.md)  
  
  
