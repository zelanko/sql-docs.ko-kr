---
description: Azure SQL DW 업로드 태스크
title: Azure SQL DW 업로드 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPDWUPTASK.F1
- sql14.dts.designer.afpdwuptask.f1
ms.assetid: eef82c89-228a-4dc7-9bd0-ea00f57692f5
author: Lingxi-Li
ms.author: lingxl
ms.openlocfilehash: a374a5eaa64eb69d96ddfe609fb8561a1dc983b6
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725987"
---
# <a name="azure-sql-dw-upload-task"></a>Azure SQL DW 업로드 태스크

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]



**Azure SQL DW 업로드 태스크**를 사용하면 SSIS 패키지가 파일 시스템이나 Azure Blob Storage에서 Azure SQL DW(Data Warehouse)로 테이블 형식 데이터를 복사할 수 있습니다.
이 태스크는 [Azure SQL Data Warehouse 로딩 패턴 및 전략](/archive/blogs/sqlcat/azure-sql-data-warehouse-loading-patterns-and-strategies) 문서에 설명된 대로 PolyBase를 활용하여 성능을 향상합니다.
현재 지원되는 원본 데이터 파일 형식은 UTF8 인코딩 방식의 구분 기호로 분리된 텍스트입니다.
파일 시스템에서 복사할 때는 먼저 준비를 위해 데이터가 Azure Blob Storage에 업로드된 후 Azure SQL DW로 업로드됩니다. 따라서 Azure Blob Storage 계정이 필요합니다.

**Azure SQL DW 업로드 태스크**는 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.

**Azure SQL DW 업로드 태스크**를 추가하려면 해당 태스크를 SSIS 도구 상자에서 디자이너 캔버스로 끌어서 놓고 두 번 클릭하거나 마우스 오른쪽 단추를 클릭하고 **편집** 을 클릭하여 태스크 편집기 대화 상자를 표시합니다.

**일반** 페이지에서 다음 속성을 구성합니다.

**SourceType**은 원본 데이터 저장소의 유형을 지정합니다. 다음 유형 중 하나를 선택합니다.

* **FileSystem:** 원본 데이터가 로컬 파일 시스템에 있습니다.
* **BlobStorage:** 원본 데이터가 Azure Blob Storage에 있습니다.

다음은 각 원본 유형의 속성입니다.

### <a name="filesystem"></a>FileSystem

필드|Description
-----|-----------
LocalDirectory|업로드할 데이터 파일이 포함된 로컬 디렉터리를 지정합니다.
Recursively|하위 디렉터리를 재귀적으로 검색할 것인지 여부를 지정합니다.
FileName|특정 이름 패턴의 파일을 선택하려면 이름 필터를 지정합니다. 예를 들어 MySheet*.xsl\* 은 MySheet001.xsl 및 MySheetABC.xslx와 같은 파일을 포함합니다.
RowDelimiter|각 행의 끝을 표시하는 문자를 지정합니다.
ColumnDelimiter|각 열의 끝을 표시하는 하나 이상의 문자를 지정합니다. 예를 들어 &#124;(파이프), \t(탭), '(작은따옴표), "(큰따옴표) 및 0x5c(백슬래시).
IsFirstRowHeader|각 데이터 파일의 첫 번째 행에 실제 데이터 대신 열 이름이 포함되는지 여부를 지정합니다.
AzureStorageConnection|Azure Storage 연결 관리자를 지정합니다.
BlobContainer|로컬 데이터가 업로드되고 PolyBase를 통해 Azure DW로 릴레이되는 Blob 컨테이너의 이름을 지정합니다. 컨테이너가 없는 경우 새 컨테이너가 만들어집니다.
BlobDirectory|로컬 데이터가 업로드되고 PolyBase를 통해 Azure DW로 릴레이되는 Blob 디렉터리(가상 계층 구조)를 지정합니다.
RetainFiles|Azure Storage에 업로드된 파일을 유지할지 여부를 지정합니다.
CompressionType|Azure Storage에 파일 업로드 시 사용할 압축 형식을 지정합니다. 로컬 원본은 영향을 받지 않습니다.
CompressionLevel|압축 형식에 사용할 압축 수준을 지정합니다.
AzureDwConnection|Azure SQL DW용 ADO.NET 연결 관리자를 지정합니다.
TableName|대상 테이블의 이름을 지정합니다. 기존 테이블 이름을 선택하거나 **\<New Table ...>** 을 선택하여 새 테이블을 만듭니다.
TableDistribution|새 테이블에 대한 배포 방법을 지정합니다. 새 테이블 이름이 **TableName**에 대해 지정된 경우 적용합니다.
HashColumnName|해시 테이블 배포에 사용되는 열을 지정합니다. **TableDistribution** 에 대해 **HASH**가 지정된 경우 적용합니다.

### <a name="blobstorage"></a>BlobStorage

필드|Description
-----|-----------
AzureStorageConnection|Azure Storage 연결 관리자를 지정합니다.
BlobContainer|원본 데이터가 있는 Blob 컨테이너의 이름을 지정합니다.
BlobDirectory|원본 데이터가 있는 Blob 디렉터리(가상 계층 구조)를 지정합니다.
RowDelimiter|각 행의 끝을 표시하는 문자를 지정합니다.
ColumnDelimiter|각 열의 끝을 표시하는 하나 이상의 문자를 지정합니다. 예를 들어 &#124;(파이프), \t(탭), '(작은따옴표), "(큰따옴표) 및 0x5c(백슬래시).
CompressionType|원본 데이터에 사용되는 압축 형식을 지정합니다.
AzureDwConnection|Azure SQL DW용 ADO.NET 연결 관리자를 지정합니다.
TableName|대상 테이블의 이름을 지정합니다. 기존 테이블 이름을 선택하거나 **\<New Table ...>** 을 선택하여 새 테이블을 만듭니다.
TableDistribution|새 테이블에 대한 배포 방법을 지정합니다. 새 테이블 이름이 **TableName**에 대해 지정된 경우 적용합니다.
HashColumnName|해시 테이블 배포에 사용되는 열을 지정합니다. **TableDistribution** 에 대해 **HASH**가 지정된 경우 적용합니다.

새 테이블 또는 기존 테이블에 복사하는지에 따라 다른 **매핑** 페이지가 표시됩니다.
새 테이블에 업로드하는 경우 매핑할 원본 열과 생성할 대상 테이블의 해당 이름을 구성합니다.
기존 테이블에 업로드하는 경우 원본 열과 대상 열 간 매핑 관계를 구성합니다.

**열** 페이지에서 각 원본 열에 대한 데이터 형식 속성을 구성합니다.

**T-SQL** 페이지에는 Azure Blob Storage에서 Azure SQL DW로 데이터를 로드하는 데 사용되는 T-SQL이 표시됩니다.
T-SQL은 다른 페이지의 구성에서 자동으로 생성되고 태스크 실행의 일부로 실행됩니다.
**편집** 단추를 클릭하여 특정 요구 사항을 충족하기 위해 생성된 T-SQL을 수동으로 편집하도록 선택할 수 있습니다.
**다시 설정** 단추를 클릭하여 자동으로 생성된 T-SQL을 나중에 되돌릴 수 있습니다.