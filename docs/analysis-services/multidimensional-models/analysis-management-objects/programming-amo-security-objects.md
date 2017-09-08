---
title: "AMO 보안 개체 프로그래밍 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- programming [AMO]
- Analysis Management Objects, security
- AMO, security
ms.assetid: 5d963721-6e6e-46eb-bc9b-18724dd0b751
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 450ae3165942cfdf290a074dd637b220e1c740d8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="programming-amo-security-objects"></a>AMO 보안 개체 프로그래밍
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], 서버 관리자 그룹 또는 Database Administrator 그룹의 구성원 보안 개체 프로그래밍 또는 AMO 보안 개체를 사용 하는 응용 프로그램을 실행 해야 합니다. Server Administrator와 Database Administrator는 액세스 수준을 제공한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 사용자는 해당 개체에 할당된 역할과 권한의 조합을 통해 가져온 모든 개체에 액세스합니다. 자세한 내용은 참조 [AMO 보안 클래스](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-security-classes.md)합니다.  
  
## <a name="role-and-permission-objects"></a>역할 및 권한 개체  
 서버 역할에는 해당 컬렉션의 유일한 역할인 관리자 역할만 있습니다. 서버 역할 컬렉션에는 새 역할을 추가할 수 없습니다. 관리자 역할의 멤버 자격에서는 서버의 모든 개체에 대한 전체 액세스를 허용합니다.  
  
 <xref:Microsoft.AnalysisServices.Role> 개체는 데이터베이스 수준에서 만들어집니다. 역할에서 멤버를 추가 또는 제거하고 역할을 <xref:Microsoft.AnalysisServices.Database> 개체에 추가 또는 제거하는 작업만으로 역할을 유지 관리할 수 있습니다. <xref:Microsoft.AnalysisServices.Permission> 개체가 연결되어 있는 역할은 삭제할 수 없습니다. 역할을 삭제하려면 먼저 <xref:Microsoft.AnalysisServices.Permission> 개체에서 모든 <xref:Microsoft.AnalysisServices.Database> 개체를 검색한 후 권한에서 <xref:Microsoft.AnalysisServices.Role>을 제거해야만 <xref:Microsoft.AnalysisServices.Role>에서 <xref:Microsoft.AnalysisServices.Database>을 삭제할 수 있습니다.  
  
 권한은 권한이 제공된 개체에서 수행할 수 있는 동작을 정의합니다. 다음 개체에 사용 권한을 제공할 수 있습니다: <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.MiningStructure>, 및 <xref:Microsoft.AnalysisServices.MiningModel>합니다. 권한 유지 관리 작업에는 해당 액세스 속성에 따라 사용 가능한 액세스를 부여 또는 취소하는 작업이 포함됩니다. 사용 가능한 각 액세스에는 원하는 액세스 수준으로 설정할 수 있는 속성이 있습니다. 액세스는 처리, 정의 읽기, 읽기, 쓰기 및 관리 작업에 대해 정의될 수 있습니다. 관리 액세스는 <xref:Microsoft.AnalysisServices.Database> 개체에만 정의됩니다. 데이터베이스 관리자 보안 수준은 역할에 데이터베이스 관리 권한이 부여된 경우에 얻을 수 있습니다.  
  
 다음 예제에서는 Database Administrators, Processors, Writers 및 Readers라는 4가지 역할을 만듭니다.  
  
 Database Administrator는 제공된 데이터베이스를 관리할 수 있습니다.  
  
 Processors는 데이터베이스의 모든 개체를 처리하고 결과를 확인할 수 있습니다. 읽기 권한은 자식 개체에 적용되지 않으므로 결과를 확인하려면 데이터베이스 개체에 대한 읽기 권한이 제공된 큐브에 대해 명시적으로 설정되어야 합니다.  
  
 Writers는 제공된 큐브를 읽고 쓸 수 있으며 셀 액세스는 Customer 차원의 'United States'로 제한됩니다.  
  
 Readers는 제공된 큐브를 읽을 수 있으며 셀 액세스는 Customer 차원의 'United States'로 제한됩니다.  
  
```  
static public void CreateRolesAndPermissions(Database db, Cube cube)  
{  
    Role role;  
    DatabasePermission dbperm;  
    CubePermission cubeperm;  
  
    #region Create the Database Administrators role  
  
    // Create the Database Administrators role.  
    role = db.Roles.Add("Database Administrators");  
    role.Members.Add(new RoleMember("")); // e.g. domain\user  
    role.Update();  
  
    // Assign administrative permissions to this role.  
    // Members of this role can perform any operation within the database.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Administer = true;  
    dbperm.Update();  
  
    #endregion  
  
    #region Create the Processors role  
  
    // Create the Processors role.  
    role = db.Roles.Add("Processors");  
    role.Members.Add(new RoleMember("")); // e.g. myDomain\johndoe  
    role.Update();  
  
    // Assign Read and Process permissions to this role.  
    // Members of this role can process objects in the database and query them to verify results.  
    // Process permission applies to all contained objects, i.e. all dimensions and cubes.  
    // Read permission does not apply to contained objects, so we must assign the permission explicitly on the cubes.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Process = true;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    cubeperm.Update();  
  
    #endregion  
  
    #region Create the Writers role  
  
    // Create the Writers role.  
    role = db.Roles.Add("Writers");  
    role.Members.Add(new RoleMember("")); // e.g. redmond\johndoe  
    role.Update();  
  
    // Assign Read and Write permissions to this role.  
    // Members of this role can discover, query and writeback to the Adventure Works cube.  
    // However cell access and writeback is restricted to the United States (in the Customer dimension).  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    cubeperm.Write = WriteAccess.Allowed;  
    cubeperm.CellPermissions.Add(new CellPermission(CellPermissionAccess.Read, "[Customer].[Country-Region].CurrentMember is [Customer].[Country-Region].[Country-Region].&[United States]"));  
    cubeperm.CellPermissions.Add(new CellPermission(CellPermissionAccess.ReadWrite, "[Customer].[Country-Region].CurrentMember is [Customer].[Country-Region].[Country-Region].&[United States]"));  
    cubeperm.Update();  
  
    #endregion  
  
    #region Create the Readers role  
  
    // Create the Readers role.  
    role = db.Roles.Add("Readers");  
    role.Members.Add(new RoleMember("")); // e.g. redmond\johndoe  
    role.Update();  
  
    // Assign Read permissions to this role.  
    // Members of this role can discover and query the Adventure Works cube.  
    // However the Customer dimension is restricted to the United States.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    Dimension dim = db.Dimensions.GetByName("Customer");  
    DimensionAttribute attr = dim.Attributes.GetByName("Country-Region");  
    CubeDimensionPermission cubedimperm = cubeperm.DimensionPermissions.Add(dim.ID);  
    cubedimperm.Read = ReadAccess.Allowed;  
    AttributePermission attrperm = cubedimperm.AttributePermissions.Add(attr.ID);  
    attrperm.AllowedSet = "{[Customer].[Country-Region].[Country-Region].&[United States]}";  
    cubeperm.Update();  
  
    #endregion  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 <xref:Microsoft.AnalysisServices>   
 [AMO 클래스 소개](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO 보안 개체 프로그래밍](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-security-objects.md)   
 [사용 권한 및 사용 권한 &#40; Analysis Services-다차원 데이터 &#41;](http://msdn.microsoft.com/library/59fa3573-f985-46cb-8042-7da71bd59a7b)   
 [논리적 아키텍처 &#40; Analysis Services-다차원 데이터 &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [데이터베이스 개체 &#40; Analysis Services-다차원 데이터 &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
