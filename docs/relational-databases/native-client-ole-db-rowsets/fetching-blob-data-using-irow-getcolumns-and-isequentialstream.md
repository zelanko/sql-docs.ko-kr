---
description: IRow::GetColumns 및 ISequentialStream을 사용하여 BLOB 데이터 인출
title: 'BLOB, IRow:: GetColumns, ISequentialStream'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching BLOB data
- ISequentialStream interface
- GetColumns method
- BLOBs, fetching
ms.assetid: b57decda-b0c1-4ef6-8c81-491956de2890
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0f842ff10b3c347daddbe1adaa04324619038e38
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97476094"
---
# <a name="fetching-blob-data-using-irowgetcolumns-and-isequentialstream"></a>IRow::GetColumns 및 ISequentialStream을 사용하여 BLOB 데이터 인출
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  다음 함수는 **IRow::GetColumns** 및 **ISequentialStream** 을 사용하여 대형 데이터를 인출합니다.  
  
```cpp
void InitializeAndExecuteCommand()  
{  
    ULONG iidx;  
    WCHAR* wCmdString=OLESTR("SELECT * FROM MyTable");  
    // Do the initialization, create the session, and set command text.  
    hr = pICommandText->Execute(NULL, IID_IRow, NULL,   
                         &cNumRows,(IUnknown **)&pIRow)))  
    //Get 1 column at a time.  
    for(ULONG i=0; i < NoOfColumns; i++)  
      GetSequentialColumn(pIRow, iidx);  
    // Do the clean up.  
}  
HRESULT GetSequentialColumn(IRow* pUnkRow, ULONG iCol)  
{  
    HRESULT hr = NOERROR;  
    ULONG cbRead = 0;  
    ULONG cbTotal = 0;  
    ULONG cColumns = 0;  
    ULONG cReads = 0;  
    ISequentialStream* pIStream = NULL;  
    WCHAR* pBuffer[kMaxBuff]; //50 chars read by ISequentialStream::Read()  
    DBCOLUMNINFO* prgInfo;  
    OLECHAR* pColNames;  
    IColumnsInfo* pIColumnsInfo;  
    DBID columnid;  
    DBCOLUMNACCESS column;  
    hr = pUnkRow->QueryInterface(IID_IColumnsInfo,   
                            (void**) &pIColumnsInfo);  
    if(FAILED(hr))  
        goto CLEANUP;  
    hr = pIColumnsInfo->GetColumnInfo(&cColumns, &prgInfo, &pColNames);  
    // Get Column ID.  
    columnid = (prgInfo + (iCol))->columnid;  
    IUnknown* pUnkStream = NULL;  
    ZeroMemory(&column, sizeof(column));  
    column.columnid = prgInfo[iCol].columnid;  
    // Ask for Iunknown interface pointer.  
    column.wType = DBTYPE_IUNKNOWN;  
    column.pData = (LPVOID*) &pUnkStream;  
  
    hr = pUnkRow->GetColumns(1, &column);  
    // Get ISequentialStream from Iunknown pointer retrieved from  
    // GetColumns().  
    hr = pUnkStream->QueryInterface(IID_ISequentialStream,   
                                   (LPVOID*) &pIStream);  
    ZeroMemory(pBuffer, kMaxBuff * sizeof(WCHAR));  
    // Read 50 chars at a time until no more data.  
    do  
    {  
        hr = pIStream->Read(pBuffer, kMaxBuff, &cbRead);  
        cbTotal = cbTotal + cbRead;  
        // Process the data.  
    } while(cbRead > 0);  
  // Do the cleanup.  
    return hr;  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [IRow를 사용하여 BLOB 데이터 인출](./fetching-a-single-row-with-irow.md)  
  
