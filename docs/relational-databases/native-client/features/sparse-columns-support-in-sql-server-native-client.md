---
title: SQL Server Native Client의 스파스 열 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sparse columns, ODBC
- sparse columns, SQL Server Native Client
- sparse columns, OLE DB
ms.assetid: aee5ed81-7e23-42e4-92d3-2da7844d9bc3
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4754553f3ceaab83497287f613fa18c5b324c4b3
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37432632"
---
# <a name="sparse-columns-support-in-sql-server-native-client"></a>SQL Server Native Client의 스파스 열 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 스파스 열을 지원합니다. 스파스 열에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 참조 하세요 [스파스 열 사용](../../../relational-databases/tables/use-sparse-columns.md) 하 고 [열 집합 사용](../../../relational-databases/tables/use-column-sets.md)합니다.  
  
 스파스 열에 대 한 자세한 내용은 지원 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 참조 하세요 [스파스 열 지원 &#40;ODBC&#41; ](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md) 하 고 [스파스 열 지원 &#40;OLE DB&#41; ](../../../relational-databases/native-client/ole-db/sparse-columns-support-ole-db.md) .  
  
 이 기능을 보여 주는 예제 응용 프로그램에 대한 자세한 내용은 [SQL Server 데이터 프로그래밍 예제](http://msftdpprodsamples.codeplex.com/)를 참조하십시오.  
  
## <a name="user-scenarios-for-sparse-columns-and-sql-server-native-client"></a>스파스 열 및 SQL Server Native Client에 대한 사용자 시나리오  
 다음 표에서는 스파스 열을 사용하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 사용자를 위한 일반적인 사용자 시나리오를 요약해서 보여 줍니다.  
  
|시나리오|동작|  
|--------------|--------------|  
|**선택 \* 테이블에서** 또는 iopenrowset:: Openrowset입니다.|스파스의 멤버가 아닌 모든 열을 반환 **column_set**, 스파스의 구성원 인 모든 null이 아닌 열의 값이 포함 된 XML 열 또한 **column_set**합니다.|  
|이름으로 열 참조|스파스 열 상태에 관계 없이 열을 참조할 수 있습니다 또는 **column_set** 멤버 자격.|  
|액세스 **column_set** 계산된 XML 열을 통해 멤버 열입니다.|스파스의 멤버인 열 **column_set** 를 선택 하 여 액세스할 수 있습니다 합니다 **column_set** 이름별 및 수 값 삽입 하 고 XML을 업데이트 하 여 업데이트를 **column_set** 열입니다.<br /><br /> 값에 대 한 스키마를 준수 해야 **column_set** 열입니다.|  
|열 검색 패턴은 NULL 또는 '%' (ODBC)를 사용 하 여 SQLColumns 통해 테이블의 모든 열에 대 한 메타 데이터 검색 또는 열 제한이 (OLE DB)를 사용 하 여 DBSCHEMA_COLUMNS 스키마 행 집합을 통해.|멤버가 아닌 모든 열에 대 한 행을 반환 된 **column_set**합니다. 이면 테이블에 스파스 **column_set**에 대 한 한 행이 반환 됩니다.<br /><br /> 멤버인 열에 대 한 메타 데이터 반환 하지 않습니다이 **column_set**합니다.|  
|스파스 또는 멤버 자격에 관계 없이 모든 열에 대 한 메타 데이터를 검색 한 **column_set**합니다. 이 경우 많은 수의 행이 반환될 수 있습니다.|설명자 필드 SQL_SOPT_SS_NAME_SCOPE를 SQL_SS_NAME_SCOPE_EXTENDED 및 호출을 설정 [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) (ODBC).<br /><br /> DBSCHEMA_COLUMNS_EXTENDED 스키마 행 집합 (OLE DB) idbschemarowset:: Getrowset을 호출 합니다.<br /><br /> 이 시나리오는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 릴리스의 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client를 사용하는 응용 프로그램에서는 사용할 수 없습니다. 그러나 이러한 응용 프로그램 시스템 뷰를 직접 쿼리할 수 있습니다.|  
|멤버인 열에 대해서만 메타 데이터를 검색 한 **column_set**합니다. 이 경우 많은 수의 행이 반환될 수 있습니다.|SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET을 설명자 필드 SQL_SOPT_SS_NAME_SCOPE를 설정 하 고 SQLColumns (ODBC)를 호출 합니다.<br /><br /> DBSCHEMA_SPARSE_COLUMN_SET 스키마 행 집합 (OLE DB)에 대 한 idbschemarowset:: Getrowset을 호출 합니다.<br /><br /> 이 시나리오는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 릴리스의 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client를 사용하는 응용 프로그램에서는 사용할 수 없습니다. 하지만 이러한 응용 프로그램은 시스템 뷰를 쿼리할 수 있습니다.|  
|열이 스파스 열인지 여부 확인|SQLColumns 결과 집합 (ODBC)의 SS_IS_SPARSE 열을 참조 하세요.<br /><br /> DBSCHEMA_COLUMNS 스키마 행 집합의 SS_IS_SPARSE 열을 확인합니다(OLE DB).<br /><br /> 이 시나리오는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 릴리스의 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client를 사용하는 응용 프로그램에서는 사용할 수 없습니다. 하지만 이러한 응용 프로그램은 시스템 뷰를 쿼리할 수 있습니다.|  
|열이를 **column_set**합니다.|SQLColumns 결과 집합의 SS_IS_COLUMN_SET 열을 참조 하세요. 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 열 특성인 SQL_CA_SS_IS_COLUMN_SET을 확인합니다(ODBC).<br /><br /> DBSCHEMA_COLUMNS 스키마 행 집합의 SS_IS_COLUMN_SET 열을 확인합니다. 또는 참조 하세요 *dwFlags* icolumnsinfo:: Getcolumninfo 또는 DBCOLUMNFLAGS icolumnsrowset:: Getcolumnsrowset에서 반환 된 행 집합에서 반환 합니다. 에 대 한 **column_set** 열의 경우 DBCOLUMNFLAGS_SS_ISCOLUMNSET이 설정 됩니다 (OLE DB).<br /><br /> 이 시나리오는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 릴리스의 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client를 사용하는 응용 프로그램에서는 사용할 수 없습니다. 하지만 이러한 응용 프로그램은 시스템 뷰를 쿼리할 수 있습니다.|  
|가져오기 및 내보내기를 사용 하 여 테이블에 대 한 BCP가 스파스 열의 **column_set**합니다.|이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 비교해서 동작이 변경되지 않았습니다.|  
|가져오기 및 내보내기 테이블의 BCP가 스파스 열을 **column_set**합니다.|**column_set** 가져오고 내보낸 XML;와 동일한 방식에서 즉,으로 **varbinary (max)** 하는 경우 또는 이진 형식으로 바인딩된 **nvarchar (max)** 경우 바인딩된를 **char** 나 **wchar** 형식입니다.<br /><br /> 스파스의 멤버인 열 **column_set** 고유한 열으로 내보내지 않은 값 으로만 내보냅니다 합니다 **column_set**합니다.|  
|**queryout** BCP에 대 한 동작입니다.|명시적으로 명명된 열의 처리 동작에 있어 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client와 비교해서 변경된 사항이 없습니다.<br /><br /> 스키마가 서로 다른 테이블 간의 가져오기 및 내보내기가 포함된 시나리오의 경우 특수 처리가 필요할 수도 있습니다.<br /><br /> BCP에 대한 자세한 내용은 이 항목의 뒤에 나오는 스파스 열에 대한 BCP(대량 복사) 지원을 참조하십시오.|  
  
## <a name="down-level-client-behavior"></a>하위 수준 클라이언트 동작  
 하위 수준 클라이언트는 스파스의 멤버가 아닌 열에 대해서만 메타 데이터를 반환 합니다 **column_set** SQLColumns 및 DBSCHMA_COLUMNS에 대 한 합니다. 에 도입 된 추가 OLE DB 스키마 행 집합 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client에 제공 되지 않으며 SQL_SOPT_SS_NAME_SCOPE 통해 odbc SQLColumns 수정 합니다.  
  
 하위 수준 클라이언트는 스파스의 멤버인 열에 액세스할 수 있습니다 **column_set** 이름별 하며 **column_set** 열에 XML 열으로 액세스할 수 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 클라이언트입니다.  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>스파스 열에 대한 BCP(대량 복사) 지원  
 스파스 열에 대 한 ODBC 또는 OLE DB의 BCP api 없는 변경 내용이 나 **column_set** 기능입니다.  
  
 테이블에는 **column_set**, 스파스 열을 별개의 열으로 처리 되지 않습니다. 모든 스파스 열 값의 값에 포함 된를 **column_set**를 동일한 방식으로 XML 열에는 내보낸,으로 **varbinary (max)** 하는 경우 또는 이진 형식으로 바인딩된  **nvarchar (max)** 경우 바인딩된를 **char** 하거나 **wchar** 형식). 가져오기에는 **column_set** 값의 스키마를 준수 해야 합니다는 **column_set**합니다.  
  
 에 대 한 **queryout** 작업을 명시적으로 참조 되는 열을 처리 하는 방식으로 변하지 않습니다. **column_set** 열 동일 하 게 동작 XML 열 및 스파스가 명명 된 스파스 열의 처리에 영향을 주지 않습니다.  
  
 그러나 경우 **queryout** 는 내보내기 하는 스파스 열 이름으로 집합의 멤버인 스파스 열을 참조에 대 한 구조가 비슷한 테이블에 직접 import를 수행할 수 없습니다. BCP 사용 메타 데이터와 일치 하기 때문에 이것이 **선택 \***  가져오기에 대 한 작업에 맞게 수 없으면 **column_set** 멤버 열이 메타이 데이터를 사용 하 여 합니다. 가져오려는 **column_set** 멤버 열 개별적으로 원하는 참조 하는 테이블에 대 한 뷰를 정의 해야 **column_set** 열을 보기를 사용 하 여 가져오기 작업을 수행 해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client 프로그래밍](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
