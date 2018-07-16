---
title: SXI(선택적 XML 인덱스) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 598ecdcd-084b-4032-81b2-eed6ae9f5d44
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 52fd8f5f58095fb53377ae1ea4bd99ca2fe15759
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202703"
---
# <a name="selective-xml-indexes-sxi"></a>SXI(선택적 XML 인덱스)
  선택적 XML 인덱스는 일반 XML 인덱스 외에 추가로 제공되는 또 다른 유형의 XML 인덱스입니다. 선택적 XML 인덱스 기능의 목적은 다음과 같습니다  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장된 XML 데이터에 대한 쿼리 성능을 향상시킵니다.  
  
-   대량의 XML 데이터 작업의 더 빠른 인덱싱을 지원합니다.'  
  
-   XML 인덱스의 저장 비용을 감소시켜 확장성을 향상시킵니다.  
  
 일반 XML 인덱스의 주요 제한 사항은 일반 인덱스는 전체 XML 문서를 인덱싱한다는 것입니다. 이로 인해 쿼리 성능 저하 및 주로 인덱스의 저장 비용과 관련된 인덱스의 유지 관리 비용 증가와 같은 몇 가지 중요한 단점이 생겨났습니다.  
  
 선택적 XML 인덱스 기능을 사용하면 특정 경로만 XML 문서에서 인덱스로 승격시킬 수 있습니다. 인덱스를 만들 때 이러한 경로가 승격되고 이러한 경로가 가리키는 노드는 분할되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관계형 테이블 내에 저장됩니다. 이 기능은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Research와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 팀이 공동으로 개발한 효율적인 매핑 알고리즘을 사용합니다. 이 알고리즘은 XML 노드를 단일 관계형 테이블에 매핑하며, 적당한 저장소 공간만을 사용하면서도 뛰어난 성능을 제공합니다.  
  
 또한 선택적 XML 인덱스 기능은 선택적 XML 인덱스에 의해 이미 인덱싱된 노드에 대해 보조 선택적 XML 인덱스를 지원합니다. 이러한 보조 선택적 인덱스는 효율적이며, 쿼리 성능을 한층 더 향상시킵니다.  
  
##  <a name="benefits"></a> 선택적 XML 인덱스의 이점  
 선택적 XML 인덱스는 다음과 같은 이점을 제공합니다.  
  
1.  일반 쿼리 부하에 비해 XML 데이터 형식에 대한 쿼리 성능이 크게 향상됩니다.  
  
2.  일반 XML 인덱스에 비해 저장소 요구 사항이 줄어듭니다.  
  
3.  일반 XML 인덱스에 비해 인덱스 유지 관리 비용이 줄어듭니다.  
  
4.  선택적 XML 인덱스를 사용하기 위해 응용 프로그램을 업데이트할 필요가 없습니다.  
  

  
##  <a name="compare"></a> 선택적 XML 인덱스 및 보조 XML 인덱스  
  
> [!IMPORTANT]  
>  대부분의 경우 더 나은 성능과 더 효율적인 저장소를 위해 일반 XML 인덱스 대신 선택적 XML 인덱스를 만듭니다.  
  
 그러나 다음 조건 중 하나에 해당하는 경우에는 선택적 XML 인덱스가 권장되지 않습니다.  
  
-   많은 수의 노드 경로를 매핑하는 경우  
  
-   문서 구조에서 알 수 없는 위치에 있는 알 수 없는 요소에 대한 쿼리를 지원하는 경우  
  

  
##  <a name="example"></a> 선택적 XML 인덱스의 간단한 예  
 테이블에 약 500,000개의 행이 있는 XML 문서인 다음 XML 조각을 살펴보십시오.  
  
```xml  
<book>  
    <created>2004-03-01</created>   
    <authors>Various</authors>  
    <subjects>  
        <subject>English wit and humor -- Periodicals</subject>  
        <subject>AP</subject>   
    </subjects>  
    <title>Punch, or the London Charivari, Volume 156, April 2, 1919</title>  
    <id>etext11617</id>  
</book>  
```  
  
 이 간단한 스키마에 있는 무수히 많은 행에 대해 주 XML 인덱스를 만들려고 하면 시간이 많이 걸립니다. 마찬가지로 주 XML 인덱스가 선택적 인덱스를 지원하지 않으므로 이 데이터를 쿼리하는 것도 쉽지 않습니다.  
  
 `/book/title` 경로 및 `/book/subjects` 경로를 통해 이 데이터를 쿼리하기만 하면 되는 경우 다음과 같은 선택적 XML 인덱스를 만들면 됩니다.  
  
```tsql  
CREATE SELECTIVE XML INDEX SXI_index  
ON Tbl(xmlcol)  
FOR   
(  
    pathTitle = '/book/title/text()' AS XQUERY 'xs:string',   
    pathAuthors = '/book/authors' AS XQUERY 'node()',  
    pathId = '/book/id' AS SQL NVARCHAR(100)  
)  
```  
  
 위의 문은 선택적 XML 인덱스를 만들 때 사용하는 CREATE 구문의 좋은 예입니다 CREATE 문에서 먼저 인덱스 수를 제공하고 인덱싱할 테이블 및 XML 열을 식별한 다음 인덱싱할 경로를 제공합니다. 경로는 다음과 같은 세 부분으로 구성되어 있습니다.  
  
1.  경로를 고유하게 식별하는 이름  
  
2.  경로를 설명하는 XQuery 식  
  
3.  선택적 최적화 힌트  
  
 이러한 요소에 대한 자세한 내용은 [관련 태스크](#reltasks)를 참조하십시오.  
  

  
## <a name="supported-features-prerequisites-and-limitations"></a>지원되는 기능, 사전 요구 사항 및 제한 사항  
  
###  <a name="features"></a> 지원되는 XML 기능  
 선택적 XML 인덱스는 exist(), value() 및 nodes() 메서드 내에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 지원하는 XQuery를 지원합니다.  
  
-   exist(), value() 및 nodes() 메서드의 경우 선택적 XML 인덱스는 전체 식을 변환할 수 있는 충분한 정보를 포함합니다.  
  
-   query() 및 modify() 메서드의 경우 선택적 XML 인덱스는 노드 필터링 목적으로만 사용될 수 있습니다.  
  
-   query() 메서드의 경우 선택적 XML 인덱스는 결과를 검색하는 데 사용되지 않습니다.  
  
-   modify() 메서드의 경우 선택적 XML 인덱스는 XML 문서를 업데이트하는 데 사용되지 않습니다.  
  

  
###  <a name="unsupported"></a> 지원되지 않는 XML 기능  
 선택적 XML 인덱스는 XML의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구현에서 지원되는 다음 기능을 지원하지 않습니다.  
  
-   공용 구조체 유형, 시퀀스 유형 및 목록 유형과 같은 복잡한 XS 유형이 있는 노드의 인덱싱  
  
-   base64Binary 및 hexBinary와 같은 이진 XS 유형이 있는 노드의 인덱싱  
  
-   끝에 `*` 와일드카드 문자가 포함된 XPath 식을 사용하여 인덱싱할 노드 지정. 예를 들면 다음과 같습니다.  `/a/b/c/*`, `/a//b/*`또는 `/a/b/*:c`  
  
-   자식, 특성 또는 하위 항목 이외의 모든 축 인덱싱. `//<step>` 은 특별한 경우로 허용됩니다.  
  
-   명령 및 주석을 처리하는 XML의 인덱싱  
  
-   id() 함수를 사용하여 노드 식별자 지정 및 검색  
  

  
###  <a name="prereq"></a> 필수 구성 요소  
 사용자 테이블의 XML 열에 대해 선택적 XML 인덱스를 만들려면 먼저 다음 사전 요구 사항을 충족해야 합니다.  
  
-   클러스터형 인덱스는 사용자 테이블의 기본 키에 있어야 합니다.  
  
-   선택적 XML 인덱스와 함께 사용할 경우 사용자 테이블의 기본 키는 128바이트로 제한됩니다.  
  
-   선택적 XML 인덱스와 함께 사용할 경우 사용자 테이블의 클러스터링 키는 15열로 제한됩니다.  
  

  
###  <a name="limits"></a> 제한 사항  
 **일반 요구 사항 및 제한 사항**  
  
-   하나의 XML 열에 대해 하나의 선택적 XML 인덱스만 만들 수 있습니다.  
  
-   XML이 아닌 열에 대해서는 선택적 XML 인덱스를 만들 수 없습니다.  
  
-   테이블의 각 XML 열에는 하나의 선택적 XML 인덱스만 지정할 수 있습니다.  
  
-   각 테이블에는 최대 249개의 선택적 XML 인덱스가 있을 수 있습니다.  
  
 **지원되는 개체에 대한 제한 사항**  
  
 다음 개체에 대해서는 선택적 XML 인덱스를 만들 수 없습니다.  
  
1.  뷰의 XML 열  
  
2.  XML 열이 있는 테이블 반환 변수  
  
3.  XML 유형 변수  
  
4.  계산된 XML 열  
  
5.  노드가 128번 이상 중첩된 XML 열  
  
 **저장소 관련 제한 사항**  
  
 XML 문서에서 인덱스에 추가할 수 있는 노드 수는 제한되어 있습니다. 선택적 XML 인덱스는 XML 문서를 하나의 관계형 테이블에 매핑합니다. 따라서 지정된 테이블의 행에는 null이 아닌 행이 1024개 이상 있을 수 없습니다. 또한 인덱스에서 저장 목적으로 스파스 열을 사용하므로 스파스 열에 대한 많은 제한 사항이 선택적 XML 열에도 적용됩니다.  
  
 지정된 행에서 지원되는 non이 아닌 열의 최대 수는 다음과 같이 열에 있는 데이터의 크기에 따라 달라집니다.  
  
-   최상의 경우에서 모든 열이 **bit**유형이면 1024개의 null이 아닌 열이 지원됩니다.  
  
-   최악의 경우에서 모든 열이 **varchar**유형의 큰 개체이면 null이 아닌 열이 236개만 지원됩니다.  
  
 선택적 XML 인덱스는 인덱싱되는 각 노드에 대해 1-4개의 열을 내부적으로 사용합니다. 인덱싱할 수 있는 총 노드 수는 인덱싱된 경로에 있는 데이터의 실제 크기에 따라 60개부터 수백 개까지 다양합니다.  
  
-   최악의 경우에서 일부 또는 모든 노드가 노드 경로 정의에 있는 `//` 코드를 사용하여 매핑되면 인덱싱되는 최대 노드 수는 60개입니다.  
  
-   최상의 경우에서 노드가 노드 경로 정의에 있는 `//` 코드를 사용하지 않고 매핑되면 인덱싱되는 최대 노드 수는 200개입니다.  
  
 **선택적 XML 인덱스는 사용자가 해당 인덱스를 만들거나 변경하면 다시 작성됩니다.**  
  
 선택적 XML 인덱스를 만들거나 변경하면 해당 인덱스는 단일 스레드 오프라인 모드에서 다시 작성됩니다. ALTER 문을 자주 실행하면 인덱싱된 XML 문서에 대한 쿼리 성능에 부정적인 영향을 줍니다.  
  
 **기타 제한 사항**  
  
-   선택적 XML 인덱스는 쿼리 힌트에서 지원되지 않습니다.  
  
-   선택적 XML 인덱스 및 보조 선택적 XML 인덱스는 데이터베이스 튜닝 관리자에서 지원되지 않습니다.  
  

  
##  <a name="reltasks"></a> 관련 작업  
  
|||  
|-|-|  
|**태스크**|**항목**|  
|선택적 XML 인덱스를 만들거나 변경할 때 인덱싱할 노드 경로 및 선택적 최적화 힌트를 지정합니다.|[선택적 XML 인덱스에 대한 경로 및 최적화 힌트 지정](specify-paths-and-optimization-hints-for-selective-xml-indexes.md)|  
|선택적 XML 인덱스를 만들고, 변경하고, 삭제합니다.|[선택적 XML 인덱스 만들기, 변경 및 삭제](create-alter-and-drop-selective-xml-indexes.md)|  
|보조 선택적 XML 인덱스를 만들고, 변경하고, 삭제합니다.|[보조 선택적 XML 인덱스 만들기, 변경 및 삭제](create-alter-and-drop-secondary-selective-xml-indexes.md)|  
  

  
  
