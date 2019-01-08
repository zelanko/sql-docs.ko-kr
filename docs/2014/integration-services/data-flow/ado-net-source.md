---
title: ADO NET 원본 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetsource.f1
helpviewer_keywords:
- ADO.NET source
- sources [Integration Services], ADO.NET
- sources [Integration Services], DataReader
- .NET Framework [Integration Services]
- DataReader source
ms.assetid: 2a2f1750-2cda-4dda-9dca-623a96a6b3c0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b672d602666fd51f98cf1854917dd2a035157d5e
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53352111"
---
# <a name="ado-net-source"></a>ADO.NET 원본
  ADO.NET 원본은 .NET 공급자의 데이터를 사용하며 데이터 흐름에서 해당 데이터를 사용할 수 있도록 합니다.  
  
 ADO NET 원본을 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에 연결할 수 있습니다. OLE DB를 사용하여 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에 연결할 수는 없습니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 대한 자세한 내용은 [일반 보안 지침 및 제한 사항(Microsoft Azure SQL Database)](https://go.microsoft.com/fwlink/?LinkId=248228)을 참조하세요.  
  
## <a name="data-type-support"></a>데이터 형식 지원  
 원본은 특정 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식에 매핑되지 않는 모든 데이터 형식을 DT_NTEXT [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식으로 변환합니다. 데이터 형식이 `System.Object`인 경우에도 이러한 변환이 발생합니다.  
  
 DT_NTEXT 데이터 형식을 DT_WSTR 데이터 형식으로 변경하거나 DT_WSTR을 DT_NTEXT로 변경할 수 있습니다. 데이터 형식을 변경하려면 ADO.NET 원본의 **고급 편집기** 대화 상자에서 **DataType** 속성을 설정하면 됩니다. 자세한 내용은 [Common Properties](../common-properties.md)을(를) 참조하세요.  
  
 ADO.NET 원본 뒤에 데이터 변환을 사용하여 DT_NTEXT 데이터 형식을 DT_BYTES 또는 DT_STR 데이터 형식으로 변환할 수도 있습니다. 자세한 내용은 [Data Conversion Transformation](transformations/data-conversion-transformation.md)을 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 날짜 데이터 형식인 DT_DBDATE, DT_DBTIME2, DT_DBTIMESTAMP2 및 DT_DBTIMESTAMPOFFSET은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 특정 날짜 데이터 형식에 매핑됩니다. ADO.NET 원본을 구성하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용되는 날짜 데이터 형식을 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 사용되는 날짜 데이터 형식으로 변환할 수 있습니다. ADO.NET 원본을 구성하여 이러한 날짜 데이터 형식을 변환하려면 **연결 관리자의** Type System Version [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 속성을 **Latest**로 설정합니다. **Type System Version** 속성은 **연결 관리자** 대화 상자의 **모두** 페이지에 있습니다. **연결 관리자** 대화 상자를 열려면 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
> [!NOTE]  
>  **연결 관리자의** Type System Version [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 속성을 **SQL Server 2005**로 설정하면 시스템은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜 데이터 형식을 DT_WSTR로 변환합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 연결 관리자가 공급자를 .NET Data Provider for [!INCLUDE[vstecado](../../includes/vstecado-md.md)] (SqlClient)로 지정하면 시스템은 UDT(사용자 정의 데이터 형식)를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] BLOB(Binary Large Object)으로 변환합니다. 시스템은 UDT 데이터 형식을 변환할 때 다음 규칙을 적용합니다.  
  
-   데이터가 큰 UDT가 아니면 시스템은 데이터를 DT_BYTES로 변환합니다.  
  
-   데이터가 큰 UDT가 아니고 데이터베이스의 열에 대한 **Length** 속성이 -1 또는 8,000바이트보다 큰 값으로 설정되어 있으면 시스템은 데이터를 DT_IMAGE로 변환합니다.  
  
-   데이터가 큰 UDT이면 시스템은 데이터를 DT_ IMAGE로 변환합니다.  
  
    > [!NOTE]  
    >  ADO.NET 원본이 오류 출력을 사용하도록 구성되지 않은 경우 시스템은 데이터를 8,000바이트 청크로 DT_IMAGE 열에 스트리밍합니다. ADO.NET 원본이 오류 출력을 사용하도록 구성된 경우에는 시스템이 전체 바이트 배열을 DT_IMAGE 열로 전달합니다. 오류 출력을 사용할 구성 요소를 구성하는 방법에 대한 자세한 내용은 [데이터의 오류 처리](error-handling-in-data.md)를 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식, 지원되는 데이터 형식 변환 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 비롯한 특정 데이터베이스에서의 데이터 형식 매핑에 대한 자세한 내용은 [Integration Services 데이터 형식](integration-services-data-types.md)을 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식을 관리 데이터 형식에 매핑하는 방법에 대한 자세한 내용은 [데이터 흐름의 데이터 형식 작업](../extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)를 참조하세요.  
  
## <a name="ado-net-source-troubleshooting"></a>ADO.NET 원본 문제 해결  
 ADO.NET 원본이 외부 데이터 공급자에 대해 수행하는 호출을 로깅할 수 있습니다. 이 로깅 기능을 사용하면 ADO.NET 원본이 외부 데이터 원본에서 데이터를 로드할 때 발생하는 문제를 해결할 수 있습니다. ADO.NET 원본이 외부 데이터 공급자에 대해 수행하는 호출을 로깅하려면 패키지 로깅을 사용하고 패키지 수준에서 **Diagnostic** 이벤트를 선택합니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.  
  
## <a name="ado-net-source-configuration"></a>ADO.NET 원본 구성  
 결과 집합을 정의하는 SQL 문을 제공하여 ADO.NET 원본을 구성합니다. 예를 들어 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 데이터베이스에 연결되고 SQL 문 `SELECT * FROM Production.Product`를 사용하는 ADO.NET 원본은 **Production.Product** 테이블에서 모든 행을 추출하고 다운스트림 구성 요소에 해당 데이터 세트를 제공합니다.  
  
> [!NOTE]  
>  SQL 문을 사용하여 임시 테이블의 결과를 반환하는 저장 프로시저를 호출하는 경우 WITH RESULT SETS 옵션을 사용하여 결과 집합의 메타데이터를 정의합니다.  
  
> [!NOTE]  
>  SQL 문을 사용하여 저장 프로시저를 실행했는데 다음 오류 메시지와 함께 작업이 실패할 경우 Exec 문 전에 `SET FMTONLY OFF` 문을 추가하여 오류를 해결할 수 있습니다.  
>   
>  **열 <열_이름>을(를) 데이터 원본에서 찾을 수 없습니다.**  
  
 ADO.NET 원본은 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 사용하여 데이터 원본에 연결하며 이 연결 관리자는 .NET 공급자를 지정합니다. 자세한 내용은 [ADO.NET Connection Manager](../connection-manager/ado-net-connection-manager.md)을(를) 참조하세요.  
  
 ADO.NET 원본에는 하나의 일반 출력과 하나의 오류 출력이 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](../common-properties.md)  
  
-   [ADO.NET 사용자 지정 속성](ado-net-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [DataReader 대상](datareader-destination.md)   
 [ADO.NET 대상](ado-net-destination.md)   
 [데이터 흐름](data-flow.md)  
  
  
