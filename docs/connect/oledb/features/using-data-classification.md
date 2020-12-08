---
title: Microsoft OLE DB Driver for SQL Server에 데이터 분류 사용 | Microsoft Docs
description: Microsoft OLE DB Driver for SQL Server를 사용하여 분류 정보를 가져오는 방법을 알아봅니다.
ms.custom: ''
ms.date: 09/30/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- OLE DB Driver for SQL Server, data classification
author: bazizi
ms.author: v-beaziz
manager: kenvh
ms.openlocfilehash: 2a46b952815fa707b03889d3f9aa6480e6e13d32
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506682"
---
# <a name="using-data-classification"></a>데이터 분류 사용
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW](../../../includes/applies-to-version/sql-asdb-asa.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="overview"></a>개요
[SQL 데이터 검색 및 분류](https://docs.microsoft.com/sql/relational-databases/security/sql-data-discovery-and-classification)는 데이터베이스에서 중요한 정보를 검색, 분류, 레이블 지정하기 위한 고급 서비스의 집합입니다. Microsoft OLE DB Driver for SQL Server(버전 [18.5.0](../release-notes-for-oledb-driver-for-sql-server.md#1850))는 기본 데이터 원본이 기능을 지원하는 경우 분류 메타데이터 검색 지원을 추가합니다. 이 정보는 [ISSDataClassification](../ole-db-interfaces/issdataclassification-ole-db.md) 인터페이스를 통해 액세스됩니다.

열에 분류를 할당하는 방법에 대한 자세한 내용은 [SQL 데이터 검색 및 분류](https://docs.microsoft.com/sql/relational-databases/security/sql-data-discovery-and-classification)를 참조하세요.

## <a name="code-samples"></a>코드 샘플

SSMS에서 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 쿼리를 실행하여 샘플 C++ 애플리케이션의 필수 구성 요소를 설정할 수 있습니다.

```sql
CREATE DATABASE [mydb]
GO

USE [mydb]
GO

CREATE TABLE [dbo].[mytable](
    [col1] [int] NULL,
    [col2] [int] NULL
)
GO

ADD SENSITIVITY CLASSIFICATION TO [dbo].[mytable].[col1] WITH (label = 'Label1', label_id = 'LabelId1', information_type = 'Type1', information_type_id = 'TypeId1', rank = Medium)
GO

ADD SENSITIVITY CLASSIFICATION TO [dbo].[mytable].[col2] WITH (label = 'Label2', label_id = 'LabelId2', information_type = 'Type2', information_type_id = 'TypeId2', rank = High)
```

다음 C++ 코드는 Microsoft OLE DB 드라이버를 사용하여 위의 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 쿼리를 사용하여 생성된 분류 정보를 가져옵니다.
```cpp
#include <atlbase.h>
#include <msdasc.h>
#include <exception>
#include <iostream>
#include <string>
#include "msoledbsql.h"

void Connect(CComPtr<IDBInitialize>& pIDBInitialize, const wchar_t* server, const wchar_t* database);
SENSITIVITYCLASSIFICATION* GetSensitivityClassificationInfo(CComPtr<IDBInitialize>& pIDBInitialize, const wchar_t* query);
void PrintSensitivityClassificationInfo(SENSITIVITYCLASSIFICATION* pSensitivityClassification);

int main()
{
    const wchar_t server[] = L"myserver";
    const wchar_t database[] = L"mydb";
    const wchar_t query[] = L"SELECT col1, col2, col1 + col2 FROM mytable";

    CoInitialize(nullptr);

    try
    {
        // Connect to data source
        CComPtr<IDBInitialize> pIDBInitialize;
        Connect(pIDBInitialize, server, database);

        // Obtain sensitivity classification info
        SENSITIVITYCLASSIFICATION* pSensitivityClassification = GetSensitivityClassificationInfo(pIDBInitialize, query);

        // Print sensitivity classification info
        PrintSensitivityClassificationInfo(pSensitivityClassification);

        if (pSensitivityClassification)
        {
            CComPtr<IMalloc> pIMalloc;
            if (FAILED(CoGetMalloc(1, &pIMalloc)))
            {
                throw std::exception("CoGetMalloc call failed.");
            }

            // Release memory
            pIMalloc->Free(pSensitivityClassification);
        }
    }
    catch (std::exception& e)
    {
        std::cerr << "Exception caught: " << e.what() << std::endl;
        return 1;
    }

    CoUninitialize();
    return 0;
}

void Connect(CComPtr<IDBInitialize>& pIDBInitialize, const wchar_t* server, const wchar_t* database)
{
    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(server) + L";Database=" +
        std::wstring(database) + L";Authentication=ActiveDirectoryIntegrated;Use Encryption for Data=true;";

    CComPtr<IDataInitialize> pIDataInitialize;
    if (FAILED(CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize))))
    {
        throw std::exception("CoCreateInstance call failed.");
    }

    if (FAILED(pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize))))
    {
        throw std::exception("GetDataSource call failed.");
    }

    if (FAILED(pIDBInitialize->Initialize()))
    {
        throw std::exception("Initialize call failed.");
    }
}

SENSITIVITYCLASSIFICATION* GetSensitivityClassificationInfo(CComPtr<IDBInitialize>& pIDBInitialize, const wchar_t* query)
{
    CComPtr<IDBCreateSession> pIDBCreateSession;
    if (FAILED(pIDBInitialize.QueryInterface<IDBCreateSession>(&pIDBCreateSession)))
    {
        throw std::exception("QueryInterface call failed.");
    }

    CComPtr<IDBCreateCommand> pIDBCreateCommand;
    if (FAILED(pIDBCreateSession->CreateSession(nullptr, IID_IDBCreateCommand, reinterpret_cast<IUnknown**>(&pIDBCreateCommand))))
    {
        throw std::exception("CreateSession call failed.");
    }

    CComPtr<ICommandText> pICommandText;
    if (FAILED(pIDBCreateCommand->CreateCommand(nullptr, IID_ICommandText, reinterpret_cast<IUnknown**>(&pICommandText))))
    {
        throw std::exception("CreateCommand call failed.");
    }

    if (FAILED(pICommandText->SetCommandText(DBGUID_DBSQL, query)))
    {
        throw std::exception("SetCommandText call failed.");
    }

    CComPtr<ISSDataClassification> pISSDataClassification;
    if (FAILED(pICommandText->Execute(nullptr, IID_ISSDataClassification, nullptr, nullptr, reinterpret_cast<IUnknown**>(&pISSDataClassification))))
    {
        throw std::exception("Execute call failed.");
    }

    SENSITIVITYCLASSIFICATION* pSensitivityClassification = nullptr;
    if (FAILED(pISSDataClassification->GetSensitivityClassification(&pSensitivityClassification)))
    {
        throw std::exception("GetSensitivityClassification call failed.");
    }

    return pSensitivityClassification;
}

void PrintSensitivityClassificationInfo(SENSITIVITYCLASSIFICATION* pSensitivityClassification)
{
    if (!pSensitivityClassification)
    {
        return;
    }

    if (pSensitivityClassification->eQuerySensitivityRank != SENSITIVITYRANK_NOT_DEFINED)
    {
        std::wcout << L"Query sensitivity rank: " << pSensitivityClassification->eQuerySensitivityRank << L"\n\n";
    }

    for (USHORT colIdx = 0; colIdx < pSensitivityClassification->cColumnSensitivityMetadata; ++colIdx)
    {
        const COLUMNSENSITIVITYMETADATA& columnMetadata = pSensitivityClassification->rgColumnSensitivityMetadata[colIdx];

        std::wcout << L"Sensitivity classification for column #" << colIdx << L":" << std::endl;
        for (USHORT propIdx = 0; propIdx < columnMetadata.cSensitivityProperties; ++propIdx)
        {
            const SENSITIVITYPROPERTY& prop = columnMetadata.rgSensitivityProperties[propIdx];

            std::wcout << L"Property #" << propIdx << L":" << std::endl;

            if (prop.eSensitivityRank != SENSITIVITYRANK_NOT_DEFINED)
            {
                std::wcout << L"\tSensitivity rank: \t" << prop.eSensitivityRank << std::endl;
            }

            if (prop.pSensitivityLabel)
            {
                if (prop.pSensitivityLabel->pwszId)
                {
                    std::wcout << L"\tSensitivity label id: \t" << prop.pSensitivityLabel->pwszId << std::endl;
                }
                if (prop.pSensitivityLabel->pwszName)
                {
                    std::wcout << L"\tSensitivity label name: " << prop.pSensitivityLabel->pwszName << std::endl;
                }
            }

            if (prop.pInformationType)
            {
                if (prop.pInformationType->pwszId)
                {
                    std::wcout << L"\tInformation type id: \t" << prop.pInformationType->pwszId << std::endl;
                }
                if (prop.pInformationType->pwszName)
                {
                    std::wcout << L"\tInformation type name: \t" << prop.pInformationType->pwszName << std::endl;
                }
            }

            std::wcout << std::endl;
        }
    }
}
```

## <a name="see-also"></a>참조
 [인터페이스&#40;OLE DB&#41;](../ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)  
 [ISSDataClassification](../ole-db-interfaces/issdataclassification-ole-db.md)  

