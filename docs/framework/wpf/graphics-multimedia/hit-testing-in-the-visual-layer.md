---
title: Hit testing a livello visivo
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hit testing functionality [WPF]
- visual layer [WPF], hit testing functionality
ms.assetid: b1a64b61-14be-4d75-b89a-5c67bebb2c7b
ms.openlocfilehash: 92b7e8ffab001af4dba6c571fd06c64f2865b1e3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962113"
---
# <a name="hit-testing-in-the-visual-layer"></a>Hit testing a livello visivo
In questo argomento vengono forniti dei cenni preliminari sulle funzionalità di hit testing fornite dal livello visivo. Il supporto per l'hit testing consente di determinare se un valore Geometry o Point rientra nel contenuto sottoposto a rendering di un oggetto <xref:System.Windows.Media.Visual>, consentendo di implementare il comportamento dell'interfaccia utente, ad esempio un rettangolo di selezione per selezionare più oggetti.  

<a name="hit_testing_scenarios"></a>   
## <a name="hit-testing-scenarios"></a>Scenari di hit Testing  
 La <xref:System.Windows.UIElement> classe fornisce il <xref:System.Windows.UIElement.InputHitTest%2A> metodo, che consente di eseguire un hit test su un elemento usando un valore di coordinata specificato. In molti casi, il <xref:System.Windows.UIElement.InputHitTest%2A> metodo fornisce la funzionalità desiderata per l'implementazione di hit testing di elementi. Esistono tuttavia diversi scenari nei quali potrebbe essere necessario implementare l'hit testing a livello visivo.  
  
- Hit testing su<xref:System.Windows.UIElement> oggetti non: Questa condizione si applica se si esegue un hit<xref:System.Windows.UIElement> testing di <xref:System.Windows.Media.DrawingVisual> oggetti non, ad esempio oggetti grafici o.  
  
- Hit testing con una geometria: Questo vale se è necessario eseguire un hit test usando un oggetto Geometry anziché il valore della coordinata di un punto.  
  
- Hit testing su più oggetti: Questo vale quando è necessario eseguire un hit test su più oggetti, ad esempio gli oggetti sovrapposti. È possibile ottenere risultati per tutti gli elementi visivi che intersecano una geometria o un punto, non solo il primo.  
  
- Il criterio di hit test verrà ignorato: <xref:System.Windows.UIElement> Questa condizione si applica quando è necessario ignorare <xref:System.Windows.UIElement> i criteri di hit testing, che prendono in considerazione i fattori che determinano se un elemento è disabilitato o invisibile.  
  
> [!NOTE]
> Per un esempio di codice completo che illustra l'hit testing a livello visivo, vedere [Hit Test Using DrawingVisuals Sample (Esempio di Hit Test mediante DrawingVisual)](https://go.microsoft.com/fwlink/?LinkID=159994) e [Hit Test with Win32 Interoperation Sample (Esempio di hit test con interoperatività Win32)](https://go.microsoft.com/fwlink/?LinkID=159995).  
  
<a name="hit_testing_support"></a>   
## <a name="hit-testing-support"></a>Supporto per Hit Testing  
 Lo scopo dei <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> metodi <xref:System.Windows.Media.VisualTreeHelper> nella classe è determinare se un valore della coordinata di geometria o punto si trova all'interno del contenuto sottoposto a rendering di un determinato oggetto, ad esempio un controllo o un elemento grafico. Ad esempio, è possibile usare l'hit testing per determinare se un clic del mouse all'interno del rettangolo di delimitazione di un oggetto avviene all'interno della geometria di un cerchio. È inoltre possibile scegliere di eseguire l'override dell'implementazione predefinita dell'hit testing per eseguire calcoli di hit testing personalizzati.  
  
 La figura seguente mostra la relazione tra l'area dell'oggetto non rettangolare e il rettangolo di delimitazione.  
  
 ![Diagramma dell'area di hit testing valida](./media/wcpsdk-mmgraphics-visuals-hittest-1.png "wcpsdk_mmgraphics_visuals_hittest_1")  
Diagramma dell'area di hit testing valida  
  
<a name="hit_testing_and_z-order"></a>   
## <a name="hit-testing-and-z-order"></a>Hit Testing e ordine Z  
 Il livello visivo di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] supporta l'hit testing su tutti gli oggetti in un punto o in una geometria, non solo sull'oggetto di primo livello. I risultati vengono restituiti nell'ordine Z. Tuttavia, l'oggetto visivo passato come parametro al metodo determina la <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> parte della struttura ad albero visuale che verrà sottoferita a hit test. È possibile sottoporre a hit testing l'intera struttura ad albero visuale o parte di essa.  
  
 Nella figura seguente, l'oggetto cerchio è sovrapposto sia al quadrato che al triangolo. Se si è interessati solo all'hit test dell'oggetto visivo il cui valore z-order è in primo piano, è possibile impostare l'enumerazione di hit test visivi in <xref:System.Windows.Media.HitTestResultCallback> modo che venga restituito <xref:System.Windows.Media.HitTestResultBehavior.Stop> da per arrestare l'attraversamento dell'hit test dopo il primo elemento.  
  
 ![Diagramma dell'ordine z&#45;di una struttura ad albero visuale](./media/wcpsdk-mmgraphics-visuals-hittest-2.png "wcpsdk_mmgraphics_visuals_hittest_2")  
Diagramma dell'ordine Z di una struttura ad albero visuale  
  
 Se si desidera enumerare tutti gli oggetti visivi in un punto o in una <xref:System.Windows.Media.HitTestResultBehavior.Continue> geometria specifici <xref:System.Windows.Media.HitTestResultCallback>, restituire da. Ciò significa che è possibile eseguire l'hit test per gli oggetti visivi che sono al di sotto di altri oggetti, anche se sono completamente nascosti. Per altre informazioni, vedere il codice di esempio nella sezione "Utilizzo del callback dei risultati di un hit test".  
  
> [!NOTE]
> Anche un oggetto visivo trasparente può essere sottoposto a hit test.  
  
<a name="using_default_hit_testing"></a>   
## <a name="using-default-hit-testing"></a>Uso dell'hit testing predefinito  
 È possibile stabilire se un punto si trova all'interno della geometria di un oggetto visivo, usando <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> il metodo per specificare un oggetto visivo e un valore di coordinata di punti su cui eseguire il test. Il parametro dell'oggetto visivo identifica il punto di avvio nella struttura ad albero visuale della ricerca dell'hit test. Se viene trovato un oggetto visivo nella struttura ad albero visuale la cui geometria contiene la coordinata, <xref:System.Windows.Media.HitTestResult.VisualHit%2A> viene impostata sulla <xref:System.Windows.Media.HitTestResult> proprietà di un oggetto. Viene quindi restituito <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> dal metodo. <xref:System.Windows.Media.HitTestResult> Se il punto non è contenuto con la sottostruttura ad albero visuale di cui si <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> esegue `null`l'hit testing, restituisce.  
  
> [!NOTE]
> L'hit testing predefinito restituisce sempre l'oggetto di livello superiore nell'ordine Z. Per identificare tutti gli oggetti visivi, compresi quelli che potrebbero essere parzialmente o completamente nascosti, usare un callback dei risultati dell'hit test.  
  
 Il valore della coordinata che viene passato come parametro <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> punto per il metodo deve essere relativo allo spazio delle coordinate dell'oggetto visivo su cui viene eseguita l'hit testing. Ad esempio, se sono presenti oggetti visivi annidati nelle coordinate (100, 100) nello spazio delle coordinate dell'elemento padre, l'hit testing su un oggetto visivo figlio con coordinate (0, 0) è equivalente all'hit testing con coordinate (100, 100) nello spazio delle coordinate dell'elemento padre.  
  
 Nel codice seguente viene illustrato come configurare i gestori di eventi del mouse per <xref:System.Windows.UIElement> un oggetto utilizzato per acquisire gli eventi utilizzati per l'hit testing.  
  
 [!code-csharp[HitTestingOverview#100](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#100)]
 [!code-vb[HitTestingOverview#100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#100)]  
  
### <a name="how-the-visual-tree-affects-hit-testing"></a>Effetti della struttura ad albero visuale sull'hit testing  
 Il punto iniziale nella struttura ad albero visuale determina quali oggetti vengono restituiti durante l'enumerazione di hit test degli oggetti. Se si dispone di più oggetti da sottoporre a hit test, l'oggetto visivo usato come punto di inizio nella struttura ad albero visuale deve essere il predecessore comune di tutti gli oggetti interessati. Se si desidera ad esempio sottoporre a hit test sia l'elemento pulsante che l'elemento visivo di disegno nel diagramma seguente, è necessario impostare il punto di inizio nella struttura ad albero visuale sul predecessore comune a entrambi. In questo caso, l'elemento canvas è il predecessore comune di sia dell'elemento pulsante che dell'elemento visivo di disegno.  
  
 ![Diagramma della gerarchia di una struttura ad albero visuale](./media/wcpsdk-mmgraphics-visuals-overview-01.gif "wcpsdk_mmgraphics_visuals_overview_01")  
Diagramma della gerarchia di una struttura ad albero visuale  
  
> [!NOTE]
> La <xref:System.Windows.UIElement.IsHitTestVisible%2A> proprietà Ottiene o imposta un valore che dichiara se un <xref:System.Windows.UIElement>oggetto derivato da può essere restituito come risultato dell'hit test da una parte del contenuto di cui è stato eseguito il rendering. In questo modo è possibile modificare selettivamente la struttura ad albero visuale per determinare quali oggetti visivi sono coinvolti in un hit test.  
  
<a name="using_a_hit_test_result_callback"></a>   
## <a name="using-a-hit-test-result-callback"></a>Uso del callback dei risultati di un hit test  
 È possibile enumerare tutti gli oggetti visivi in una struttura ad albero visuale la cui geometria contiene un valore di coordinate specificato. Ciò consente di identificare tutti gli oggetti visivi, inclusi quelli che potrebbero essere parzialmente o completamente nascosti da altri oggetti visivi. Per enumerare gli oggetti visivi in una struttura <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> ad albero visuale, usare il metodo con una funzione di callback dell'hit test. La funzione di callback dell'hit test viene chiamata dal sistema quando il valore delle coordinate specificato è contenuto in un oggetto visivo.  
  
 Durante l'enumerazione dei risultati dell'hit test, evitare di eseguire operazioni che modifichino la struttura ad albero visuale. L'aggiunta o la rimozione di un oggetto dalla struttura ad albero visuale mentre viene attraversata può produrre un comportamento imprevedibile. È possibile modificare in modo sicuro la struttura ad <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> albero visuale dopo che il metodo restituisce. È possibile fornire una struttura di dati, ad esempio <xref:System.Collections.ArrayList>, per archiviare i valori durante l'enumerazione dei risultati dell'hit test.  
  
 [!code-csharp[HitTestingOverview#101](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#101)]
 [!code-vb[HitTestingOverview#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#101)]  
  
 Il metodo di callback dell'hit test definisce le azioni eseguite quando viene identificato un hit test su un determinato oggetto visivo nella struttura ad albero visuale. Dopo aver eseguito le azioni, viene restituito un <xref:System.Windows.Media.HitTestResultBehavior> valore che determina se continuare l'enumerazione di altri oggetti visivi.  
  
 [!code-csharp[HitTestingOverview#102](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#102)]
 [!code-vb[HitTestingOverview#102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#102)]  
  
> [!NOTE]
> L'ordine di enumerazione di oggetti visivi di hit testing è l'ordine Z. L'oggetto visivo di livello superiore nell'ordine Z viene enumerato per primo. Gli altri oggetti visivi vengono enumerati a livelli decrescenti nell'ordine Z. Questo ordine di enumerazione corrisponde all'ordine di rendering degli oggetti visivi.  
  
 È possibile arrestare l'enumerazione degli oggetti visivi in qualsiasi momento nella funzione di callback dell'hit test <xref:System.Windows.Media.HitTestResultBehavior.Stop>restituendo.  
  
 [!code-csharp[HitTestingOverview#103](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#103)]
 [!code-vb[HitTestingOverview#103](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#103)]  
  
<a name="using_a_hit_test_filter_callback"></a>   
## <a name="using-a-hit-test-filter-callback"></a>Uso del callback di un filtro dell'hit test  
 È possibile usare un filtro dell'hit test facoltativo per limitare gli oggetti inviati ai risultati dell'hit test. Ciò consente di ignorare parti della struttura ad albero visuale che non si desidera elaborare nei risultati dell'hit test. Per implementare un filtro di hit test, è necessario definire una funzione di callback del filtro dell'hit test e passarla come valore di <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> parametro quando si chiama il metodo.  
  
 [!code-csharp[HitTestingOverview#104](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#104)]
 [!code-vb[HitTestingOverview#104](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#104)]  
  
 Se non si vuole fornire la funzione di callback del filtro di hit test facoltativo, passare `null` un valore come parametro per il <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> metodo.  
  
 [!code-csharp[HitTestingOverview#105](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#105)]
 [!code-vb[HitTestingOverview#105](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#105)]  
  
 ![Eliminazione di una struttura ad albero visuale con un filtro hit test](./media/filteredvisualtree-01.png "FilteredVisualTree_01")  
Eliminazione di una struttura ad albero visuale  
  
 La funzione di callback del filtro dell'hit test consente di enumerare tutti gli oggetti visivi il cui contenuto di rendering include le coordinate specificate. È possibile tuttavia decidere di ignorare determinate parti della struttura ad albero visuale che non si desidera elaborare nella funzione di callback dei risultati dell'hit test. Il valore restituito dalla funzione di callback del filtro dell'hit test determina il tipo di azione che deve essere eseguita dall'enumerazione degli oggetti visivi. Se, ad esempio, si restituisce il valore <xref:System.Windows.Media.HitTestFilterBehavior.ContinueSkipSelfAndChildren>, è possibile rimuovere l'oggetto visivo corrente e i relativi elementi figlio dall'enumerazione dei risultati dell'hit test. Ciò significa che la funzione di callback dei risultati di hit test non visualizzerà questi oggetti nell'enumerazione. L'eliminazione di oggetti dalla struttura ad albero visuale consente di ridurre la quantità di elaborazione durante la fase di enumerazione dei risultati dell'hit test. Nell'esempio di codice seguente il filtro ignora le etichette e i relativi discendenti e sottopone a hit test tutti gli altri elementi.  
  
 [!code-csharp[HitTestingOverview#106](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#106)]
 [!code-vb[HitTestingOverview#106](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#106)]  
  
> [!NOTE]
> Verrà talvolta chiamato il callback del filtro dell'hit test nei casi in cui non viene chiamato il callback di risultati dell'hit test.  
  
<a name="overriding_default_hit_testing"></a>   
## <a name="overriding-default-hit-testing"></a>Override dell'hit testing predefinito  
 È possibile eseguire l'override del supporto per l'hit testing predefinito di un <xref:System.Windows.Media.Visual.HitTestCore%2A> oggetto visivo eseguendo l'override del metodo. Ciò significa che quando si richiama il <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> metodo, viene chiamata l'implementazione sottoposta a override di. <xref:System.Windows.Media.Visual.HitTestCore%2A> Il metodo sottoposto a override viene chiamato quando un hit test viene eseguito all'interno del rettangolo delimitatore dell'oggetto visivo, anche se le coordinate non rientrano nel contenuto sottoposto a rendering dell'oggetto visivo.  
  
 [!code-csharp[HitTestingOverview#107](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#107)]
 [!code-vb[HitTestingOverview#107](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#107)]  
  
 È possibile che si desideri eseguire un hit test sia sul rettangolo di delimitazione, sia sul contenuto di rendering di un oggetto visivo. Usando il `PointHitTestParameters` valore del parametro nel metodo sottoposto <xref:System.Windows.Media.Visual.HitTestCore%2A> a override come parametro per il metodo <xref:System.Windows.Media.Visual.HitTestCore%2A>di base, è possibile eseguire azioni in base a un hit del rettangolo delimitatore di un oggetto visivo e quindi eseguire un secondo hit test sulla contenuto sottoposto a rendering dell'oggetto visivo.  
  
 [!code-csharp[HitTestingOverview#108](~/samples/snippets/csharp/VS_Snippets_Wpf/HitTestingOverview/CSharp/Window1.xaml.cs#108)]
 [!code-vb[HitTestingOverview#108](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HitTestingOverview/visualbasic/window1.xaml.vb#108)]  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A>
- <xref:System.Windows.Media.HitTestResult>
- <xref:System.Windows.Media.HitTestResultCallback>
- <xref:System.Windows.Media.HitTestFilterCallback>
- <xref:System.Windows.UIElement.IsHitTestVisible%2A>
- [Hit test con l'esempio DrawingVisuals](https://go.microsoft.com/fwlink/?LinkID=159994)
- [Esempio di hit test con interoperatività Win32](https://go.microsoft.com/fwlink/?LinkID=159995)
- [Eseguire un hit test della geometria in un oggetto Visual](how-to-hit-test-geometry-in-a-visual.md)
- [Eseguire un hit test utilizzando un contenitore di host Win32](how-to-hit-test-using-a-win32-host-container.md)
