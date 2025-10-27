**Directiva estructural**

`@Directive({`
	`standalone: true,`
	`selector: '[appShownOnScreenSize]'`
`})`
`export class appShownOnScreenSizeDirective implements OnInit {`
	`@Input() appShownOnScreenSize: 'small' | 'medium' | 'large';`
	
	constructor(){
		private templateRef: TemplateRef<any>,
		private viewContainer: ViewContainerRef
	}
	
	ngOnInit(){
		
	}
`}`

Aplicación

`<div *appShownOnScreenSize="'small'"> Contenido para pantallas pequeñas </ div>`

---

**Directiva atributo**

- `ElementRef` → Nos devuelve el elemento al cual se le aplicó la directiva.
- `Renderer2` → Nos permite manipular elementos del DOM. **(como sus estilos, clases, etc.)**

`@Directive({`
	`standalone: true,`
	`selector: "[appHighLight]"`
`})`
`export class HighLightDirective {`

	constructor(private el: ElementRef, private renderer: Renderer2){
	}
	
	@HostListener("mouseenter") onMouseEnter(){`
		this.renderer.setStyle(this.el.nativeElement, "background-color", "yellow" );
	}
	
	@HostListener("mouseleave") onMouseLeave(){
		this.renderer.removeStyle(this.el.nativeElement, "background-color");
	}
`}`

Aplicación

`<p appHighLight> Pasa el mouse sobre este texto para resaltar su contenido. </ p>`