---
title: 대량 데이터 가져오기 (Native Client OLE DB 공급자) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- DBPROP_ACCESSORDER property
- SQL Server Native Client OLE DB provider, BLOBs
- large data, OLE objects
ms.assetid: a31c5632-96aa-483f-a307-004c5149fbc0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 298a442dbb93ca2c0bb95d79e341d712cd3651ea
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243686"
---
# <a name="getting-large-data-from-a-sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 공급자에서 대량 데이터 가져오기
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  일반적으로 소비자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ISequentialStream** 인터페이스 포인터를 통해 참조 되지 않는 데이터를 처리 하는 다른 코드에서 네이티브 클라이언트 OLE DB 공급자 저장소 개체를 만드는 코드를 격리 해야 합니다.  
  
 이 항목에서는 다음 함수와 함께 사용할 수 있는 기능에 대해 설명합니다.  
  
-   IRowset:GetData  
  
-   IRow::GetColumns  
  
-   ICommand::Execute  
  
 행 집합 속성 그룹의 DBPROP_ACCESSORDER 속성이 DBPROPVAL_AO_SEQUENTIAL 또는 DBPROPVAL_AO_SEQUENTIALSTORAGEOBJECTS 값 중 하나로 설정 된 경우, BLOB 데이터가 버퍼링 되지 않으므로 소비자는 **GetNextRows** 메서드를 호출 하 여 데이터의 단일 행만 인출 해야 합니다. DBPROP_ACCESSORDER 값이 DBPROPVAL_AO_RANDOM으로 설정되어 있으면 소비자가 **GetNextRows**에서 여러 데이터 행을 인출할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 소비자가 요청할 때까지에서 대량 데이터를 검색 하지 않습니다. 소비자는 모든 소규모 데이터를 하나의 접근자에 바인딩한 다음 필요에 따라 하나 이상의 임시 접근자를 사용하여 대규모 데이터 값을 검색해야 합니다.  
  
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
    // The SQL Server Native Client OLE DB provider.  
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
 [Blob 및 OLE 개체](../../relational-databases/native-client-ole-db-blobs/blobs-and-ole-objects.md)   
 [큰 값 형식 사용](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
