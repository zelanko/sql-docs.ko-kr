---
title: 사용자 지정 보고서 항목 디자인 타임 구성 요소 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- custom report items, creating
ms.assetid: 323fd58a-a462-4c48-b188-77ebc0b4212e
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 03d555f967b50b503d608244bdd4a8885cede61e
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025864"
---
# <a name="creating-a-custom-report-item-design-time-component"></a>사용자 지정 보고서 항목 디자인 타임 구성 요소 만들기
  사용자 지정 보고서 항목 디자인 타임 구성 요소는 Visual Studio 보고서 디자이너 환경에서 사용할 수 있는 컨트롤입니다. 사용자 지정 보고서 항목 디자인 타임 구성 요소는 끌어서 놓기 작업이 가능하고 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 속성 브라우저와 통합되고 사용자 지정 속성 편집기를 제공하는 활성화된 디자인 화면을 제공합니다.  
  
 사용자 지정 보고서 항목 디자인 타임 구성 요소를 사용하여 사용자는 디자인 환경에서 보고서에 사용자 지정 보고서 항목을 배치하고, 사용자 지정 보고서 항목에 사용자 지정 데이터 속성을 설정한 다음, 사용자 지정 보고서 항목을 보고서 프로젝트의 일부로 저장할 수 있습니다.  
  
 개발 환경에서 디자인 타임 구성 요소를 사용하여 설정된 속성은 호스트 디자인 환경에 의해 serialize 및 deserialize된 다음 RDL(Report Definition Language) 파일에 요소로 저장됩니다. 보고서 처리기에 의해 보고서가 실행되면, 디자인 타임 구성 요소를 사용하여 설정된 속성을 보고서 처리기가 사용자 지정 보고서 항목 런타임 구성 요소로 전달하고, 이 런타임 구성 요소는 사용자 지정 보고서 항목을 렌더링한 뒤 다시 보고서 처리기로 전달합니다.  
  
> [!NOTE]  
>  사용자 지정 보고서 항목 디자인 타임 구성 요소는 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 구성 요소로 구현됩니다. 이 문서에서는 사용자 지정 보고서 항목 디자인 타임 구성 요소와 관련된 구현 세부 사항을 설명합니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]를 사용하여 구성 요소를 개발하는 방법은 MSDN 라이브러리에서 [Visual Studio의 구성 요소](https://go.microsoft.com/fwlink/?LinkId=116576)를 참조하십시오.  
  
 완전히 구현된 사용자 지정 보고서 항목 예는 [SQL Server Reporting Services 제품 예제](https://go.microsoft.com/fwlink/?LinkId=177889)를 참조하세요.  
  
## <a name="implementing-a-design-time-component"></a>디자인 타임 구성 요소 구현  
 사용자 지정 보고서 항목 디자인 타임 구성 요소의 주 클래스는 `Microsoft.ReportDesigner.CustomReportItemDesigner` 클래스에서 상속됩니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 컨트롤에 사용된 표준 특성 외에, 구성 요소 클래스에서 `CustomReportItem` 특성을 정의해야 합니다. 이 특성은 reportserver.config 파일에 정의된 사용자 지정 보고서 항목의 이름과 일치해야 합니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 특성 목록은 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 설명서에서 "특성(Attributes)"을 참조하십시오.  
  
 다음 코드 예제는 사용자 지정 보고서 항목 디자인 타임 컨트롤에 적용되는 특성을 보여 줍니다.  
  
```csharp  
namespace PolygonsCRI  
{  
    [LocalizedName("Polygons")]  
    [Editor(typeof(CustomEditor), typeof(ComponentEditor))]  
        [ToolboxBitmap(typeof(PolygonsDesigner),"Polygons.ico")]  
        [CustomReportItem("Polygons")]  
  
    public class PolygonsDesigner : CustomReportItemDesigner  
    {  
...  
```  
  
### <a name="initializing-the-component"></a>구성 요소 초기화  
 <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> 클래스를 사용하여 사용자 지정 보고서 항목에 대해 사용자가 지정한 속성을 전달합니다. `CustomReportItemDesigner` 클래스 구현에서 `InitializeNewComponent` 메서드를 무시하고 구성 요소 <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> 클래스의 새 인스턴스를 만들어 이를 기본값으로 설정해야 합니다.  
  
 다음 코드 예제는 `CustomReportItemDesigner.InitializeNewComponent` 메서드를 무시하고 구성 요소의 <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> 클래스를 초기화하는 사용자 지정 보고서 항목 디자인 타임 구성 요소 클래스의 예를 보여 줍니다.  
  
```csharp  
public override void InitializeNewComponent()  
        {  
            CustomData = new CustomData();  
            CustomData.DataRowHierarchy = new DataHierarchy();  
  
            // Shape grouping  
            CustomData.DataRowHierarchy.DataMembers.Add(new DataMember());  
            CustomData.DataRowHierarchy.DataMembers[0].Group = new Group();  
            CustomData.DataRowHierarchy.DataMembers[0].Group.Name = Name + "_Shape";  
            CustomData.DataRowHierarchy.DataMembers[0].Group.GroupExpressions.Add(new ReportExpression());  
  
            // Point grouping  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers.Add(new DataMember());  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group = new Group();  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group.Name = Name + "_Point";  
            CustomData.DataRowHierarchy.DataMembers[0].DataMembers[0].Group.GroupExpressions.Add(new ReportExpression());  
  
            // Static column  
            CustomData.DataColumnHierarchy = new DataHierarchy();  
            CustomData.DataColumnHierarchy.DataMembers.Add(new DataMember());  
  
            // Points  
            IList<IList<DataValue>> dataValues = new List<IList<DataValue>>();  
            CustomData.DataRows.Add(dataValues);  
            CustomData.DataRows[0].Add(new List<DataValue>());  
            CustomData.DataRows[0][0].Add(NewDataValue("X", ""));  
            CustomData.DataRows[0][0].Add(NewDataValue("Y", ""));  
        }  
```  
  
### <a name="modifying-component-properties"></a>구성 요소 속성 수정  
 디자인 환경에서 여러 가지 방법으로 `CustomData` 속성을 수정할 수 있습니다. [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 속성 브라우저를 사용하여 <xref:System.ComponentModel.BrowsableAttribute> 특성으로 표시된, 디자인 타임 구성 요소에서 노출한 속성을 수정할 수 있습니다. 또한 사용자 지정 보고서 항목의 디자인 화면으로 항목을 끌어 오거나, 디자인 환경에서 컨트롤을 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 **속성**을 선택하여 사용자 지정 속성 창을 표시하는 방법으로 속성을 수정할 수 있습니다.  
  
 다음 코드 예제는 <xref:System.ComponentModel.BrowsableAttribute> 특성이 적용된 `Microsoft.ReportDesigner.CustomReportItemDesigner.CustomData` 속성을 보여 줍니다.  
  
```csharp  
[Browsable(true), Category("Data")]  
public string DataSetName  
{  
      get  
      {  
         return CustomData.DataSetName;  
      }  
      set  
      {  
         CustomData.DataSetName = value;  
      }  
   }  
  
```  
  
 디자인 타임 구성 요소를 사용자 지정 속성 편집기 대화 상자로 제공할 수 있습니다. 사용자 지정 속성 편집기 구현은 <xref:System.ComponentModel.ComponentEditor> 클래스에서 상속해야 하며, 속성 편집에 사용할 수 있는 대화 상자 인스턴스를 만들어야 합니다.  
  
 다음 예제는 <xref:System.ComponentModel.ComponentEditor>에서 상속되어 사용자 지정 속성 편집기 대화 상자를 표시하는 클래스의 구현을 보여 줍니다.  
  
```csharp  
internal sealed class CustomEditor : ComponentEditor  
{  
   public override bool EditComponent(  
      ITypeDescriptorContext context, object component)  
    {  
     PolygonsDesigner designer = (PolygonsDesigner)component;  
     PolygonProperties dialog = new PolygonProperties();  
     dialog.m_designerComponent = designer;  
     DialogResult result = dialog.ShowDialog();  
     if (result == DialogResult.OK)  
     {  
        designer.Invalidate();  
        designer.ChangeService().OnComponentChanged(designer, null, null, null);  
        return true;  
     }  
     else  
        return false;  
    }  
}  
```  
  
 사용자 지정 속성 편집기 대화 상자에서 보고서 디자이너 식 편집기를 호출할 수 있습니다. 다음 예제에서는 사용자가 콤보 상자에서 첫 번째 요소를 선택하면 식 편집기가 호출됩니다.  
  
```csharp  
private void EditableCombo_SelectedIndexChanged(object sender,   
    EventArgs e)  
{  
   ComboBox combo = (ComboBox)sender;  
   if (combo.SelectedIndex == 0 && m_launchEditor)  
   {  
      m_launchEditor = false;  
      ExpressionEditor editor = new ExpressionEditor();  
      string newValue;  
      newValue = (string)editor.EditValue(null, m_designerComponent.Site, m_oldComboValue);  
      combo.Items[0] = newValue;  
   }  
}  
  
```  
  
### <a name="using-designer-verbs"></a>디자이너 동사 사용  
 디자이너 동사는 이벤트 처리기에 연결 된 메뉴 명령입니다. 사용자 지정 보고서 항목 런타임 컨트롤이 디자인 환경에서 사용될 때 구성 요소의 바로 가기 메뉴에 표시할 디자이너 동사를 추가할 수 있습니다. `Verbs` 속성을 사용하여 런타임 구성 요소에서 사용 가능한 디자이너 동사 목록을 반환할 수 있습니다.  
  
 다음 코드 예제는 <xref:System.ComponentModel.Design.DesignerVerbCollection>에 추가할 디자이너 동사 및 이벤트 처리기와 이벤트 처리기 코드를 보여 줍니다.  
  
```csharp  
public override DesignerVerbCollection Verbs  
{  
    get  
    {  
        if (m_verbs == null)  
        {  
            m_verbs = new DesignerVerbCollection();  
            m_verbs.Add(new DesignerVerb("Proportional Scaling", new EventHandler(OnProportionalScaling)));  
         m_verbs[0].Checked = (GetCustomProperty("poly:Proportional") == bool.TrueString);  
        }  
  
        return m_verbs;  
    }  
}  
  
private void OnProportionalScaling(object sender, EventArgs e)  
{  
   bool proportional = !  
        (GetCustomProperty("poly:Proportional") == bool.TrueString);  
   m_verbs[0].Checked = proportional;  
   SetCustomProperty("poly:Proportional", proportional.ToString());  
   ChangeService().OnComponentChanged(this, null, null, null);  
   Invalidate();  
}  
```  
  
### <a name="using-adornments"></a>도구 영역(adornment) 사용  
 사용자 지정 보고서 항목 클래스는 `Microsoft.ReportDesigner.Design.Adornment` 클래스도 구현할 수 있습니다. 도구 영역(adornment)을 사용하면 사용자 지정 보고서 항목 컨트롤의 주 사각형 디자인 화면 바깥에 일정 영역이 생깁니다. 이 영역은 마우스 클릭 및 끌어서 놓기 작업과 같은 사용자 인터페이스 이벤트를 처리할 수 있습니다. `Adornment` 에 정의 된 클래스를 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] `Microsoft.ReportDesigner` 네임 스페이스의 통과 구현입니다는 <xref:System.Windows.Forms.Design.Behavior.Adorner> Windows Forms에 있는 클래스입니다. 에 대 한 전체 설명서는 `Adorner` 클래스를 참조 하십시오 [동작 서비스 개요](https://go.microsoft.com/fwlink/?LinkId=116673) MSDN 라이브러리에서. 구현 하는 샘플 코드를 `Microsoft.ReportDesigner.Design.Adornment` 클래스를 참조 하십시오 [SQL Server Reporting Services 제품 예제](https://go.microsoft.com/fwlink/?LinkId=177889)합니다.  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서 Windows Forms를 프로그래밍하고 사용하는 방법은 MSDN Library에서 다음 항목을 참조하십시오.  
  
-   구성 요소의 디자인 타임 특성  
  
-   [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]의 구성 요소  
  
-   연습: Visual Studio의 디자인 타임 기능을 사용하는 Windows Forms 컨트롤 만들기  
  
## <a name="see-also"></a>관련 항목  
 [사용자 지정 보고서 항목 아키텍처](custom-report-item-architecture.md)   
 [사용자 지정 보고서 항목 런타임 구성 요소 만들기](creating-a-custom-report-item-run-time-component.md)   
 [사용자 지정 보고서 항목 클래스 라이브러리](custom-report-item-class-libraries.md)   
 [방법: 사용자 지정 보고서 항목 배포](how-to-deploy-a-custom-report-item.md)  
  
  
