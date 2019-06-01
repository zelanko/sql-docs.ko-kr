---
title: Foreach 루프 편집기 (컬렉션 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.collection.f1
ms.assetid: 95a19dde-61ca-4d9b-aa3d-131fa4264296
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5b9396ab5a25bba979859ac685c4759b8b01c24d
ms.sourcegitcommit: 5905c29b5531cef407b119ebf5a120316ad7b713
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66428803"
---
# <a name="foreach-loop-editor-collection-page"></a>Foreach 루프 편집기(컬렉션 페이지)
  **Foreach 루프 편집기** 대화 상자의 **컬렉션** 페이지를 사용하여 열거자 유형을 지정하고 열거자를 구성할 수 있습니다.  
  
 Foreach 루프 컨테이너와 이를 구성하는 방법은 [Foreach 루프 컨테이너](control-flow/foreach-loop-container.md) 및 [Foreach 루프 컨테이너 구성](../../2014/integration-services/configure-a-foreach-loop-container.md)을 참조하세요.  
  
## <a name="static-options"></a>정적 옵션  
 **Enumerator**  
 목록에서 열거자 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**Foreach File 열거자**|파일을 열거합니다. 이 값을 선택하면 아래의 **Foreach File 열거자**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**Foreach Item 열거자**|항목의 값을 열거합니다. 이 값을 선택하면 아래의 **Foreach Item 열거자**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**Foreach ADO 열거자**|테이블 또는 테이블의 행을 열거합니다. 이 값을 선택하면 아래의 **Foreach ADO 열거자**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**Foreach ADO.NET 스키마 행 집합 열거자**|스키마를 열거합니다. 이 값을 선택하면 아래의 **Foreach ADO.NET 열거자**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**Foreach From Variable 열거자**|변수의 값을 열거합니다. 이 값을 선택하면 아래의 **Foreach From Variable 열거자**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**Foreach Nodelist 열거자**|XML 문서의 노드를 열거합니다. 이 값을 선택하면 아래의 **Foreach Nodelist 열거자**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**Foreach SMO 열거자**|SMO 개체를 열거합니다. 이 값을 선택하면 아래의 **Foreach SMO 열거자**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**Foreach Azure Blob 열거자**|지정된 Blob 위치에 있는 Blob 파일을 열거합니다. 이 값을 선택하면 **Foreach Azure Blob 열거자**섹션에 동적 옵션이 표시됩니다.|  
|**Foreach ADLS File 열거자**|필터를 사용 하 여 ADLS에 파일을 열거 합니다. 이 값을 선택하면 **Foreach ADLS File 열거자**섹션에 동적 옵션이 표시됩니다.|
  
 **식**  
 기존 속성 식 목록을 보려면 **식** 을 클릭 또는 확장합니다. 줄임표 단추 **(...)** 를 클릭하여 열거자 속성에 대한 속성 식을 추가하거나 기존 속성 식을 편집 및 평가합니다.  
  
 **관련 항목:**  [Integration Services&#40;SSIS&#41; 식](expressions/integration-services-ssis-expressions.md), [속성 식 편집기](expressions/property-expressions-editor.md), [식 작성기](expressions/expression-builder.md)  
  
## <a name="enumerator-dynamic-options"></a>Enumerator 동적 옵션  
  
### <a name="enumerator--foreach-file-enumerator"></a>Enumerator = Foreach File 열거자  
 폴더의 파일을 열거하는 데 Foreach File 열거자를 사용할 수 있습니다. 예를 들어 Foreach 루프가 SQL 실행 태스크를 포함하는 경우 Foreach File 열거자를 사용하여 SQL 실행 태스크에서 실행하는 SQL 문을 포함하는 파일을 열거할 수 있습니다. 하위 폴더를 포함하도록 열거자를 구성할 수 있습니다.  
  
 루프의 외부 프로세스 또는 태스크에서는 루프가 실행되는 동안 파일을 추가, 삭제하거나 파일 이름을 바꾸기 때문에 Foreach File 열거자가 열거하는 폴더 및 하위 폴더의 내용이 루프가 실행되는 동안 변경될 수 있습니다. 즉, 다음과 같은 예기치 않은 상황이 발생할 수 있습니다.  
  
-   파일을 삭제한 경우 Foreach 루프의 특정 태스크에서 후속 태스크에 사용되는 파일과 다른 파일 집합에 태스크를 수행할 수 있습니다.  
  
-   파일 이름이 바뀌어 외부 프로세스에서 이름이 바뀐 파일을 대체하기 위해 자동으로 파일을 추가한 경우 Foreach 루프가 같은 파일 내용에 대해 작업을 두 번 수행할 수 있습니다.  
  
-   파일을 추가한 경우 Foreach 루프가 작업을 수행한 파일을 확인하기 어려울 수 있습니다.  
  
 **Folder**  
 열거할 루트 폴더의 경로를 입력합니다.  
  
 **찾아보기**  
 루트 폴더를 찾으려면 클릭합니다.  
  
 **파일**  
 열거할 파일을 지정합니다.  
  
> [!NOTE]  
>  와일드카드 문자(*)를 사용하여 컬렉션에 포함할 파일을 지정합니다. 예를 들어 이름에 “abc”가 포함된 파일을 포함하려면 \*abc\* 필터를 사용합니다.  
>   
>  파일 이름 확장명을 지정하면 열거자는 동일한 확장명에 추가 문자가 포함된 파일도 반환합니다. 이 동작은 이전 버전과의 호환성을 위해 8.3 파일 이름도 비교하는 운영 체제의 **dir** 명령줄 동작과 같습니다. 이 열거자 동작으로 인해 예기치 못한 결과가 발생할 수 있습니다. 예를 들어 Excel 2003 파일만 열거하기 위해 "*.xls"를 지정하면 열거자는 Excel 2007 파일도 반환합니다. 이는 Excel 2007 파일의 확장명이 ".xlsx"이기 때문입니다.  
>   
>  식을 사용하여 컬렉션에 포함할 파일을 지정할 수 있습니다. **컬렉션** 페이지에서 **식**을 확장하고 **FileSpec** 속성을 선택한 다음, 줄임표 단추(...)를 클릭하여 속성 식을 추가합니다. 동적으로 지정 된 파일을 선택 하는 방법에 대 한 자세한 내용은 참조 하세요. [SSIS-동적으로 파일 마스크 설정: FileSpec](https://rajsudeep.blogspot.com/2010/09/ssisdynamically-set-file-mask-filespec.html)  
  
 **정규화된 이름**  
 파일 이름의 정규화된 경로를 검색하려면 선택합니다. 파일 옵션에서 와일드카드 문자를 지정한 경우 반환된 정규화된 경로가 필터와 일치합니다.  
  
 **이름만**  
 파일 이름만 검색하려면 선택합니다. 파일 옵션에서 와일드카드 문자를 지정하지 않은 경우 반환된 파일 이름이 필터와 일치합니다.  
  
 **이름 및 확장명**  
 파일 이름 및 해당 파일 이름 확장명을 검색하려면 선택합니다. 파일 옵션에서 와일드카드 문자를 지정한 경우 반환된 파일의 이름과 확장명이 필터와 일치합니다.  
  
 **하위 폴더 포함**  
 열거에 하위 폴더를 포함하려면 선택합니다.  
  
### <a name="enumerator--foreach-item-enumerator"></a>Enumerator = Foreach Item 열거자  
 컬렉션의 항목을 열거하는 데 Foreach Item 열거자를 사용할 수 있습니다. 열 및 열 값을 지정하여 컬렉션의 항목을 정의합니다. 행의 열은 항목을 정의합니다. 예를 들어 프로세스 실행 태스크에서 실행하는 실행 파일과 해당 태스크에서 사용하는 작업 디렉터리를 지정하는 항목에는 두 개의 열, 즉 실행 파일의 이름을 나열하는 열과 작업 디렉터리를 나열하는 열이 있습니다. 행 수는 루프가 반복되는 횟수를 결정합니다. 테이블에 10개의 행이 있는 경우 루프는 10번 반복됩니다.  
  
 프로세스 실행 태스크의 속성을 업데이트하려면 열의 인덱스를 사용하여 변수를 항목 열에 매핑합니다. 인덱스 값은 열거자 항목에 정의된 첫 번째 열에 0, 두 번째 열에 1과 같이 열에 순서대로 지정됩니다. 변수 값은 루프가 반복될 때마다 업데이트됩니다. 그런 다음 프로세스 실행 태스크의 `Executable` 및 `WorkingDirectory` 속성은 이러한 변수를 사용하는 속성 식으로 업데이트할 수 있습니다.  
  
 **For Each Item 컬렉션에 항목 정의**  
 테이블의 각 열에 대한 값을 입력합니다.  
  
> [!NOTE]  
>  행 열에 값을 입력하면 새 행이 해당 테이블에 자동으로 추가됩니다.  
  
> [!NOTE]  
>  입력한 값이 열 데이터 형식과 호환되지 않으면 텍스트가 빨간색으로 표시됩니다.  
  
 **열 데이터 형식**  
 활성 열의 데이터 형식을 나열합니다.  
  
 **제거**  
 목록에서 항목을 제거하려면 항목을 선택하고 **제거** 를 클릭합니다.  
  
 **열**  
 항목에 있는 열의 데이터 형식을 구성하려면 클릭합니다.  
  
 **관련 항목:** [For Each Item 열 대화 상자 UI 참조](../../2014/integration-services/for-each-item-columns-dialog-box-ui-reference.md)  
  
### <a name="enumerator--foreach-ado-enumerator"></a>Enumerator = Foreach ADO 열거자  
 변수에 저장된 ADO 또는 ADO.NET 개체의 행이나 테이블을 열거하는 데 Foreach ADO 열거자를 사용할 수 있습니다. 예를 들어 Foreach 루프가 변수에 데이터 세트를 기록하는 스크립트 태스크를 포함하는 경우 Foreach ADO 열거자를 사용하여 데이터 세트의 행을 열거할 수 있습니다. 변수가 ADO.NET 데이터 세트를 포함하는 경우 여러 테이블의 행을 열거하거나 테이블을 열거하도록 열거자를 구성할 수 있습니다.  
  
 **ADO 개체 원본 변수**  
 목록에서 사용자 정의 변수를 선택하거나 \<**새 변수...** >를 클릭하여 새 변수를 만듭니다.  
  
> [!NOTE]  
>  변수에 Object 데이터 형식이 있어야 합니다. 그렇지 않으면 오류가 발생합니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
 **첫 번째 테이블의 행**  
 첫 번째 테이블의 행만 열거하려면 선택합니다.  
  
 **모든 테이블의 행(ADO.NET 데이터 집합에만 해당)**  
 모든 테이블의 행을 열거하려면 선택합니다. 이 옵션은 열거할 모든 개체가 같은 ADO.NET 데이터 세트의 멤버인 경우에만 사용할 수 있습니다.  
  
 **모든 테이블(ADO.NET 데이터 집합에만 해당)**  
 테이블만 열거하려면 선택합니다.  
  
### <a name="enumerator--foreach-adonet-schema-rowset-enumerator"></a>Enumerator = Foreach ADO.NET 스키마 행 집합 열거자  
 지정한 데이터 원본에 대한 스키마를 열거하는 데 Foreach ADO.NET 스키마 행 집합 열거자를 사용할 수 있습니다. 예를 들어 Foreach 루프가 SQL 실행 태스크를 포함하는 경우 Foreach ADO.NET 스키마 행 집합 열거자를 사용하여 **AdventureWorks** 데이터베이스의 열과 같은 스키마를 열거하고 SQL 실행 태스크를 사용하여 스키마 사용 권한을 가져올 수 있습니다.  
  
 **대량 삽입 태스크 편집기**  
 목록에서 ADO.NET 연결 관리자를 선택하거나 \<**새 연결...** >을 클릭하여 새 ADO.NET 연결 관리자를 만듭니다.  
  
> [!IMPORTANT]  
>  ADO.NET 연결 관리자는 OLE DB용 .NET 공급자를 사용해야 합니다. SQL Server에 연결하는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 연결 관리자 **대화 상자의** OleDb용 .NET 공급자 **섹션에 나열된** Native Client를 공급자로 사용하는 것이 좋습니다.  
  
 **관련 항목:** [ADO 연결 관리자](connection-manager/ado-connection-manager.md), [ADO.NET 연결 관리자 구성](configure-ado-net-connection-manager.md)  
  
 **스키마**  
 열거할 스키마를 선택합니다.  
  
 **제한 설정**  
 지정한 스키마에 적용할 제한을 설정합니다.  
  
 **관련 항목:** [스키마 제한 대화 상자](../../2014/integration-services/schema-restrictions-dialog-box.md)  
  
### <a name="enumerator--foreach-from-variable-enumerator"></a>Enumerator = Foreach From Variable 열거자  
 지정한 변수의 열거 가능한 개체를 열거하는 데 Foreach From Variable 열거자를 사용할 수 있습니다. 예를 들어 Foreach 루프가 쿼리를 실행하여 변수에 결과를 저장하는 SQL 실행 태스크를 포함하는 경우 Foreach From Variable 열거자를 사용하여 쿼리 결과를 열거할 수 있습니다.  
  
 **변수**  
 목록에서 변수를 선택하거나 \<**새 변수...** >를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
### <a name="enumerator--foreach-nodelist-enumerator"></a>Enumerator = Foreach NodeList 열거자  
 XML 파일에 XPath 식을 적용한 결과 생성된 XML 노드 집합을 열거하는 데 Foreach Nodelist 열거자를 사용할 수 있습니다. 예를 들어 Foreach 루프가 스크립트 태스크를 포함하는 경우 Foreach NodeList 열거자를 사용하여 XPath 식 조건에 부합하는 값을 XML 파일에서 스크립트 태스크로 전달할 수 있습니다.  
  
 XML 파일에 적용되는 XPath 식은 OuterXPathString 속성에 저장되는 외부 XPath 작업입니다. XPath 열거형으로 설정 된 경우 `ElementCollection`, Foreach NodeList 열거자는 InnerXPathString 속성 요소의 컬렉션을에 저장 되는 내부 XPath 식을 적용할 수 있습니다.  
  
 XML 문서 및 데이터 작업 방법은 MSDN Library의 "[.NET Framework에 XML 적용(Employing XML in the .NET Framework)](https://go.microsoft.com/fwlink/?LinkId=56214)"을 참조하십시오.  
  
 **DocumentSourceType**  
 XML 문서의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 **DocumentSource**  
 **DocumentSourceType**을 **직접 입력**으로 설정한 경우 XML 코드를 입력하거나 줄임표(...) 단추를 클릭하고 **문서 원본 편집기** 대화 상자를 사용하여 XML을 입력합니다.  
  
 **DocumentSourceType**을 **파일 연결**로 설정한 경우 파일 연결 관리자를 선택하거나 \<**새 연결...** >을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **DocumentSourceType**을 **변수**로 설정한 경우 기존 변수를 선택하거나 \<**새 변수...** >를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
 **EnumerationType**  
 목록에서 열거 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**Navigator**|XPathNavigator를 사용하여 열거합니다.|  
|**Node**|XPath 작업에서 반환한 노드를 열거합니다.|  
|**NodeText**|XPath 작업에서 반환한 텍스트 노드를 열거합니다.|  
|`ElementCollection`|XPath 작업에서 반환한 요소 노드를 열거합니다.|  
  
 **OuterXPathStringSourceType**  
 XPath 문자열의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 `OuterXPathString`  
 **OuterXPathStringSourceType**을 **직접 입력**으로 설정한 경우 XPath 문자열을 입력합니다.  
  
 **OuterXPathStringSourceType**을 **파일 연결**로 설정한 경우 파일 연결 관리자를 선택하거나 \<**새 연결...** >을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **OuterXPathStringSourceType**을 **변수**로 설정한 경우 기존 변수를 선택하거나 \<**새 변수...** >를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
 **InnerElementType**  
 하는 경우 **EnumerationType** 로 설정 된 `ElementCollection`, 목록에서 내부 요소의 유형을 선택 합니다.  
  
 **InnerXPathStringSourceType**  
 내부 XPath 문자열의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**직접 입력**|원본을 XML 문서로 설정합니다.|  
|**파일 연결**|XML 문서가 포함된 파일을 선택합니다.|  
|**변수**|원본을 XML 문서가 포함된 변수로 설정합니다.|  
  
 `InnerXPathString`  
 **InnerXPathStringSourceType**을 **직접 입력**으로 설정한 경우 XPath 문자열을 입력합니다.  
  
 **InnerXPathStringSourceType**을 **파일 연결**로 설정한 경우 파일 연결 관리자를 선택하거나 \<**새 연결...** >을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **InnerXPathStringSourceType**을 **변수**로 설정한 경우 기존 변수를 선택하거나 \<**새 변수...** >를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md), [변수 추가](../../2014/integration-services/add-variable.md)  
  
### <a name="enumerator--foreach-smo-enumerator"></a>Enumerator = Foreach SMO 열거자  
 SMO(SQL Server Management Objects) 개체를 열거하는 데 Foreach SMO 열거자를 사용할 수 있습니다. 예를 들어 Foreach 루프가 SQL 실행 태스크를 포함하는 경우 Foreach SMO 열거자를 사용하여 **AdventureWorks** 데이터베이스의 테이블을 열거하고 각 테이블의 행 수를 계산하는 쿼리를 실행할 수 있습니다.  
  
 **대량 삽입 태스크 편집기**  
 기존 ADO.NET 연결 관리자를 선택하거나 \<**새 연결...** >을 클릭하여 새 연결 관리자를 만듭니다.  
  
 관련 항목: [ADO.NET 연결 관리자](connection-manager/ado-net-connection-manager.md), [ADO.NET 연결 관리자 구성](configure-ado-net-connection-manager.md)  
  
 **열거**  
 열거할 SMO 개체를 지정합니다.  
  
 **찾아보기**  
 SMO 열거를 선택합니다.  
  
 **관련 항목:** [SMO 열거 선택 대화 상자](../../2014/integration-services/select-smo-enumeration-dialog-box.md)  
  
### <a name="enumerator--foreach-azure-blob-enumerator"></a>열거자 = Foreach Azure Blob 열거자  
 **Azure Blob 열거자**를 사용하면 SSIS 패키지에서 지정된 Blob 위치에 있는 Blob 파일을 열거할 수 있습니다. 열거된 Blob 파일의 이름을 변수에 저장하여 Foreach 루프 컨테이너 내의 작업에서 사용할 수 있습니다.  
  
 **Azure Storage 연결 관리자**  
 기존 Azure Storage 연결 관리자를 선택하거나 Azure Storage 계정을 참조하는 연결 관리자 하나를 새로 만듭니다.  
  
 관련 항목: [Azure Storage 연결 관리자](connection-manager/azure-storage-connection-manager.md).  
  
 **Blob 컨테이너 이름**  
 열거할 Blob 파일을 포함하는 Blob 컨테이너의 이름을 지정합니다.  
  
 **Blob 디렉터리**  
 열거할 Blob 파일을 포함하는 Blob 디렉터리를 지정합니다. Blob 디렉터리는 가상 계층 구조입니다.  
  
 **Blob 이름 필터**  
 특정 이름 패턴의 파일을 열거하려면 이름 필터를 지정합니다. 예를 들어 MySheet*.xls\* 는 MySheet001.xls 및 MySheetABC.xlsx와 같은 파일을 포함합니다.  
  
 **Blob 시간 범위 시작/끝 필터**  
 시간 범위 필터를 지정합니다. **TimeRangeFrom** 에서 **TimeRangeTo** 사이에 수정된 파일이 열거됩니다.  
### <a name="enumerator--foreach-adls-file-enumerator"></a>열거자 = Foreach ADLS File 열거자  
합니다 **ADLS File 열거자** 필터를 사용 하 여 ADLS에 파일을 열거 하는 SSIS 패키지를 사용 하도록 설정 합니다. 슬래시 (`/`)-열거 되는 파일의 전체 경로 접두사를 변수에 저장 하 고 Foreach 루프 컨테이너 내의 작업에 사용 되는 수입니다.
  
**AzureDataLakeConnection**  
Azure Data Lake 연결 관리자를 지정하거나 ADLS 계정을 참조하는 새 연결 관리자를 만듭니다.   
  
**AzureDataLakeDirectory**  
검색할 ADLS 디렉터리를 지정 합니다.
  
**FileNamePattern**  
파일 이름 필터를 지정합니다. 이름이 지정된 된 패턴과 일치 하는 파일만 열거 됩니다. 와일드카드 `*` 및 `?`가 지원됩니다. 
  
**SearchRecursively**  
지정된 디렉터리 내에서 재귀적으로 검색할 것인지 지정합니다.  
  
## <a name="external-resources"></a>외부 리소스  
  
-   bidn.com의 블로그 항목 - [각 노드 목록 열거자에 대한 SSIS](https://go.microsoft.com/fwlink/?LinkId=220671)  
  
-   블로그 항목, [SSIS-동적으로 파일 마스크 설정: FileSpec](https://rajsudeep.blogspot.com/2010/09/ssisdynamically-set-file-mask-filespec.html).  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Foreach 루프 편집기 &#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [Foreach 루프 편집기 &#40;변수 매핑 페이지&#41;](../../2014/integration-services/foreach-loop-editor-variable-mappings-page.md)   
 [식 페이지](expressions/expressions-page.md)   
 [For 루프 컨테이너](control-flow/for-loop-container.md)  
  
  
