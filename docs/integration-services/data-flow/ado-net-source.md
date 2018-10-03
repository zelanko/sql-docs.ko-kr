---
title: ADO NET 원본 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetsource.f1
- sql13.dts.designer.adonetsource.connection.f1
- sql13.dts.designer.adonetsource.columns.f1
- sql13.dts.designer.adonetsource.erroroutput.f1
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
ms.openlocfilehash: 8ca0a56e3168e5493104cd54472516800d444078
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47665587"
---
# <a name="ado-net-source"></a>ADO.NET 원본
  ADO.NET 원본은 .NET 공급자의 데이터를 사용하며 데이터 흐름에서 해당 데이터를 사용할 수 있도록 합니다.  
  
 ADO NET 원본을 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]에 연결할 수 있습니다. OLE DB를 사용하여 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에 연결할 수는 없습니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 대한 자세한 내용은 [일반 보안 지침 및 제한 사항(Microsoft Azure SQL Database)](http://go.microsoft.com/fwlink/?LinkId=248228)을 참조하세요.  
  
## <a name="data-type-support"></a>데이터 형식 지원  
 원본은 특정 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식에 매핑되지 않는 모든 데이터 형식을 DT_NTEXT [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식으로 변환합니다. 데이터 형식이 **System.Object**인 경우에도 이러한 변환이 발생합니다.  
  
 DT_NTEXT 데이터 형식을 DT_WSTR 데이터 형식으로 변경하거나 DT_WSTR을 DT_NTEXT로 변경할 수 있습니다. 데이터 형식을 변경하려면 ADO.NET 원본의 **고급 편집기** 대화 상자에서 **DataType** 속성을 설정하면 됩니다. 자세한 내용은 [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)을(를) 참조하세요.  
  
 ADO.NET 원본 뒤에 데이터 변환을 사용하여 DT_NTEXT 데이터 형식을 DT_BYTES 또는 DT_STR 데이터 형식으로 변환할 수도 있습니다. 자세한 내용은 [Data Conversion Transformation](../../integration-services/data-flow/transformations/data-conversion-transformation.md)을 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 날짜 데이터 형식인 DT_DBDATE, DT_DBTIME2, DT_DBTIMESTAMP2 및 DT_DBTIMESTAMPOFFSET은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 특정 날짜 데이터 형식에 매핑됩니다. ADO.NET 원본을 구성하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용되는 날짜 데이터 형식을 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 사용되는 날짜 데이터 형식으로 변환할 수 있습니다. ADO.NET 원본을 구성하여 이러한 날짜 데이터 형식을 변환하려면 **연결 관리자의** Type System Version [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 속성을 **Latest**로 설정합니다. **Type System Version** 속성은 **연결 관리자** 대화 상자의 **모두** 페이지에 있습니다. **연결 관리자** 대화 상자를 열려면 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
> [!NOTE]  
>  **연결 관리자의** Type System Version [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 속성을 **SQL Server 2005**로 설정하면 시스템은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜 데이터 형식을 DT_WSTR로 변환합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 연결 관리자가 공급자를 .NET Data Provider for [!INCLUDE[vstecado](../../includes/vstecado-md.md)] (SqlClient)로 지정하면 시스템은 UDT(사용자 정의 데이터 형식)를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] BLOB(Binary Large Object)으로 변환합니다. 시스템은 UDT 데이터 형식을 변환할 때 다음 규칙을 적용합니다.  
  
-   데이터가 큰 UDT가 아니면 시스템은 데이터를 DT_BYTES로 변환합니다.  
  
-   데이터가 큰 UDT가 아니고 데이터베이스의 열에 대한 **Length** 속성이 -1 또는 8,000바이트보다 큰 값으로 설정되어 있으면 시스템은 데이터를 DT_IMAGE로 변환합니다.  
  
-   데이터가 큰 UDT이면 시스템은 데이터를 DT_ IMAGE로 변환합니다.  
  
    > [!NOTE]  
    >  ADO.NET 원본이 오류 출력을 사용하도록 구성되지 않은 경우 시스템은 데이터를 8,000바이트 청크로 DT_IMAGE 열에 스트리밍합니다. ADO.NET 원본이 오류 출력을 사용하도록 구성된 경우에는 시스템이 전체 바이트 배열을 DT_IMAGE 열로 전달합니다. 오류 출력을 사용할 구성 요소를 구성하는 방법에 대한 자세한 내용은 [데이터의 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식, 지원되는 데이터 형식 변환 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 비롯한 특정 데이터베이스에서의 데이터 형식 매핑에 대한 자세한 내용은 [Integration Services 데이터 형식](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식을 관리 데이터 형식에 매핑하는 방법에 대한 자세한 내용은 [데이터 흐름의 데이터 형식 작업](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)를 참조하세요.  
  
## <a name="ado-net-source-troubleshooting"></a>ADO.NET 원본 문제 해결  
 ADO.NET 원본이 외부 데이터 공급자에 대해 수행하는 호출을 로깅할 수 있습니다. 이 로깅 기능을 사용하면 ADO.NET 원본이 외부 데이터 원본에서 데이터를 로드할 때 발생하는 문제를 해결할 수 있습니다. ADO.NET 원본이 외부 데이터 공급자에 대해 수행하는 호출을 로깅하려면 패키지 로깅을 사용하고 패키지 수준에서 **Diagnostic** 이벤트를 선택합니다. 자세한 내용은 [패키지 실행 문제 해결 도구](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)를 참조하세요.  
  
## <a name="ado-net-source-configuration"></a>ADO.NET 원본 구성  
 결과 집합을 정의하는 SQL 문을 제공하여 ADO.NET 원본을 구성합니다. 예를 들어 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 데이터베이스에 연결되고 SQL 문 `SELECT * FROM Production.Product` 를 사용하는 ADO.NET 원본은 **Production.Product** 테이블에서 모든 행을 추출하고 다운스트림 구성 요소에 해당 데이터 집합을 제공합니다.  
  
> [!NOTE]  
>  SQL 문을 사용하여 임시 테이블의 결과를 반환하는 저장 프로시저를 호출하는 경우 WITH RESULT SETS 옵션을 사용하여 결과 집합의 메타데이터를 정의합니다.  
  
> [!NOTE]  
>  SQL 문을 사용하여 저장 프로시저를 실행했는데 다음 오류 메시지와 함께 작업이 실패할 경우 Exec 문 앞에 **SET FMTONLY OFF** 문을 추가하여 오류를 해결할 수 있습니다.  
>   
>  **열 <열_이름>을(를) 데이터 원본에서 찾을 수 없습니다.**  
  
 ADO.NET 원본은 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 사용하여 데이터 원본에 연결하며 이 연결 관리자는 .NET 공급자를 지정합니다. 자세한 내용은 [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)을(를) 참조하세요.  
  
 ADO.NET 원본에는 하나의 일반 출력과 하나의 오류 출력이 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [ADO.NET 사용자 지정 속성](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="ado-net-source-editor-connection-manager-page"></a>ADO NET 원본 편집기(연결 관리자 페이지)
  **ADO NET 원본 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 원본의 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자를 선택할 수 있습니다. 이 페이지를 사용하면 데이터베이스에서 테이블이나 뷰를 선택할 수도 있습니다.  
  
 ADO NET 원본에 대한 자세한 내용은 [ADO NET Source](../../integration-services/data-flow/ado-net-source.md)을 참조하십시오.  
  
 **연결 관리자 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 ADO NET 원본이 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 ADO NET 원본을 두 번 클릭합니다.  
  
3.  **ADO NET 원본 편집기**에서 **연결 관리자**를 클릭합니다.  
  
### <a name="static-options"></a>정적 옵션  
 **ADO.NET 연결 관리자**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **ADO.NET 연결 관리자 구성** 대화 상자를 사용하여 새 연결 관리자를 만듭니다.  
  
 **데이터 액세스 모드**  
 원본에서 데이터를 선택하는 방법을 지정합니다.  
  
|옵션|설명|  
|------------|-----------------|  
|테이블 또는 뷰|[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 데이터 원본에 있는 테이블이나 뷰에서 데이터를 검색합니다.|  
|SQL 명령|SQL 쿼리를 사용하여 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 데이터 원본에서 데이터를 검색합니다.|  
  
 **미리 보기**  
 **데이터 보기** 대화 상자를 사용하여 결과를 미리 봅니다. **미리 보기** 에는 최대 200개의 행이 표시될 수 있습니다.  
  
> [!NOTE]  
>  데이터를 미리 보면 CLR 사용자 정의 형식의 열에 데이터가 포함되지 않습니다. 대신 \<값이 너무 커서 표시할 수 없습니다> 또는 System.Byte[] 값이 표시됩니다. 전자는 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 공급자를 사용하여 데이터 원본에 액세스하는 경우 표시되고 후자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 공급자를 사용하는 경우 표시됩니다.  
  
### <a name="data-access-mode-dynamic-options"></a>데이터 액세스 모드 동적 옵션  
  
#### <a name="data-access-mode--table-or-view"></a>데이터 액세스 모드 = 테이블 또는 뷰  
 **테이블 또는 뷰 이름**  
 데이터 원본의 사용 가능한 테이블 또는 뷰 목록에서 테이블 또는 뷰 이름을 선택합니다.  
  
#### <a name="data-access-mode--sql-command"></a>데이터 액세스 모드 = SQL 명령  
 **SQL 명령 텍스트**  
 SQL 쿼리 텍스트를 입력하고 **쿼리 작성**을 클릭하여 쿼리를 작성하거나 **찾아보기**를 클릭하여 쿼리 텍스트가 포함된 파일을 찾습니다.  
  
 **쿼리 작성**  
 **쿼리 작성기** 대화 상자를 사용하여 시각적으로 SQL 쿼리를 생성할 수 있습니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 SQL 쿼리 텍스트가 포함된 파일을 찾을 수 있습니다.  
  
## <a name="ado-net-source-editor-columns-page"></a>ADO NET 원본 편집기(열 페이지)
  **ADO NET 원본 편집기** 대화 상자의 **열** 페이지를 사용하여 출력 열을 각 외부(원본) 열에 매핑할 수 있습니다.  
  
 ADO NET 원본에 대한 자세한 내용은 [ADO NET Source](../../integration-services/data-flow/ado-net-source.md)을 참조하십시오.  
  
 **열 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 ADO NET 원본이 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 ADO NET 원본을 두 번 클릭합니다.  
  
3.  **ADO NET 원본 편집기**에서 **열**을 클릭합니다.  
  
### <a name="options"></a>Options  
 **사용 가능한 외부 열**  
 데이터 원본에서 사용 가능한 외부 열의 목록을 표시합니다. 이 테이블을 사용하여 열을 추가하거나 삭제할 수 없습니다.  
  
 **외부 열**  
 이 원본의 데이터를 사용하는 구성 요소를 구성할 때 표시되는 순서로 외부(원본) 열을 표시합니다.  
  
 **출력 열**  
 각 출력 열에 고유한 이름을 지정합니다. 기본값은 선택한 외부(원본) 열의 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다. 제공한 이름은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
## <a name="ado-net-source-editor-error-output-page"></a>ADO NET 원본 편집기(오류 출력 페이지)
  **ADO NET 원본 편집기** 대화 상자의 **오류 출력** 페이지를 사용하여 오류 처리 옵션을 선택하고 오류 출력 열에 속성을 설정할 수 있습니다.  
  
 ADO NET 원본에 대한 자세한 내용은 [ADO NET Source](../../integration-services/data-flow/ado-net-source.md)을 참조하십시오.  
  
 **오류 출력 페이지를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 ADO NET 원본이 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 ADO NET 원본을 두 번 클릭합니다.  
  
3.  **ADO NET 원본 편집기**에서 **오류 출력**을 클릭합니다.  
  
### <a name="options"></a>Options  
 **입/출력**  
 데이터 원본의 이름을 표시합니다.  
  
 **열**  
 **ADO NET 원본 편집기** 대화 상자의 **연결 관리자** 페이지에서 선택한 외부(원본) 열을 표시합니다.  
  
 **오류**  
 오류가 발생할 경우 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **관련 항목:** [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **잘림**  
 잘림이 발생할 경우 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **설명**  
 오류에 대한 설명을 표시합니다.  
  
 **이 값을 선택한 셀에 설정**  
 오류나 잘림 발생 시 선택한 모든 셀에 수행할 동작을 지정합니다. 오류 무시, 행 리디렉션 또는 구성 요소 실패를 지정할 수 있습니다.  
  
 **적용**  
 선택한 셀에 오류 처리 옵션을 적용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [DataReader 대상](../../integration-services/data-flow/datareader-destination.md)   
 [ADO.NET 대상](../../integration-services/data-flow/ado-net-destination.md)   
 [데이터 흐름](../../integration-services/data-flow/data-flow.md)  
  
  
