---
title: "SQL Server 가져오기 및 내보내기 마법사에서 데이터 형식 매핑 | Microsoft Docs"
ms.custom: 
ms.date: 01/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 669be403-cb17-4b12-bbbf-e7a74003c4b6
caps.latest.revision: 2
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4eca10e506087ee5d8106cb05c861c4efa49a65d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="data-type-mapping-in-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사에서 데이터 형식 매핑
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서는 새로운 대상 테이블 및 파일에서 열의 이름, 데이터 형식 및 데이터 형식 속성을 설정할 수 있지만 열 값에 대한 사용자 지정 변환을 지정할 수는 없습니다. 결과적으로, 원본-대상 간의 기본 제공 데이터 형식 매핑이 중요합니다.  
  
##  <a name="wizardMapping"></a> 마법사가 원본과 대상 간에 데이터 형식을 매핑하는 방법
마법사에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 설치한 매핑 파일을 사용하여 데이터베이스 시스템 또는 버전 간에 데이터 형식을 매핑합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 Oracle 데이터 형식으로 매핑할 수 있습니다. 기본적으로 XML 형식의 매핑 파일은 다음 폴더에 설치됩니다.
-   **C:\Program Files\Microsoft SQL Server\130\DTSMappingFiles\**  (64 비트용)
-   **C:\Program 파일 (x86) \Microsoft SQL Server\130\DTSMappingFiles\**  (32 비트)에 대 한 합니다.  
  
 기존 매핑 파일을 편집하거나 새 매핑 파일을 폴더에 추가할 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 닫았다가 다시 열어야 새 파일 또는 변경된 파일이 인식됩니다.  
 
## <a name="you-can-change-an-existing-mapping-file"></a>기존 매핑 파일을 변경할 수 있습니다.
비즈니스에서 데이터 형식 간에 다른 매핑을 필요로 하는 경우 매핑 파일을 업데이트하여 마법사가 사용하는 매핑을 변경할 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 DB2로 데이터를 전송할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **nchar** 데이터 형식이 DB2 **VARGRAPHIC** 데이터 형식 대신 DB2 **GRAPHIC** 데이터 형식에 매핑되도록 하려면 **SqlClientToIBMDB2.xml** 매핑 파일에서 **nchar** 매핑을 변경하여 **VARGRAPHIC** 대신 **GRAPHIC**을 사용하도록 합니다.  
  
## <a name="you-can-add-a-new-mapping-file"></a>새 매핑 파일을 추가할 수 있습니다.
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 원본 및 대상에 일반적으로 사용되는 조합 간의 매핑을 설치합니다. **MappingFiles** 디렉터리에 매핑 파일을 추가하여 추가 원본 및 대상을 지원할 수도 있습니다. 새 매핑 파일은 게시된 XSD 스키마를 따라야 하며 원본과 대상의 고유한 조합 간에 매핑해야 합니다. 매핑 파일용 스키마 **DataTypeMapping.xsd**는 [여기](http://schemas.microsoft.com/sqlserver/2008/07/IntegrationServices/DataTypeMapping/DataTypeMapping.xsd)에 게시됩니다.
 
## <a name="sample-mapping-file"></a>예제 매핑 파일
다음은 SQL Server 데이터 형식(또는 .Net Framework Data Provider for SQL Server에서 사용되는 데이터 형식)에서 Oracle 데이터 형식으로 매핑하는 XML 매핑 파일의 일부입니다. 예를 들어 SQL Server **int** 데이터 형식을 Oracle **INTEGER** 데이터 형식에 매핑할 수 있습니다.
  
```xml  
  
<dtm:DataTypeMappings  
    xmlns:dtm="http://www.microsoft.com/SqlServer/Dts/DataTypeMapping.xsd"   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    SourceType="System.Data.SqlClient.SqlConnection"   
    MinSourceVersion="*"   
    MaxSourceVersion="*"   
    DestinationType="MSDAORA;OraOLEDB.Oracle;System.Data.OracleClient.OracleConnection"   
    MinDestinationVersion="08.*"   
    MaxDestinationVersion="*">  
  
    <!-- smallint -->  
    <dtm:DataTypeMapping >  
        <dtm:SourceDataType>  
            <dtm:DataTypeName>smallint</dtm:DataTypeName>  
        </dtm:SourceDataType>  
        <dtm:DestinationDataType>  
            <dtm:SimpleType>  
                <dtm:DataTypeName>INTEGER</dtm:DataTypeName>  
            </dtm:SimpleType>  
        </dtm:DestinationDataType>  
    </dtm:DataTypeMapping>    
  
    <!-- int -->  
    <dtm:DataTypeMapping >  
        <dtm:SourceDataType>  
            <dtm:DataTypeName>int</dtm:DataTypeName>  
        </dtm:SourceDataType>  
        <dtm:DestinationDataType>  
            <dtm:SimpleType>  
                <dtm:DataTypeName>INTEGER</dtm:DataTypeName>  
            </dtm:SimpleType>  
        </dtm:DestinationDataType>  
    </dtm:DataTypeMapping>    
  
        ...  
  
</dtm:DataTypeMappings>  
  
```  


