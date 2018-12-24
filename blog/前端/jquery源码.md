<h1 align='center'><font color=red>jquery源码</font></h1>

### 一、$
$是jquery关键字的缩写，在jquery源码的开头定义了一个自调用的匿名方法
```javascript
(function( global, factory ) {
	if ( typeof module === "object" && typeof module.exports === "object" ) {
		module.exports = global.document ?
			factory( global, true ) :
			function( w ) {
				if ( !w.document ) {
					throw new Error( "jQuery requires a window with a document" );
				}
				return factory( w );
			};
	} else {
		factory( global );
	}
}(typeof window !== "undefined" ? window : this, function( window, noGlobal ) {
  ……
  ……
  if ( !noGlobal ) {
	   window.jQuery = window.$ = jQuery;
  }
}
```
有且仅有 CommonJS标准环境下，存在窗口时并 module.exports = global.document 条件成立时，$ 不为jquery对象。

### 二、构造函数
```javascript
  var jQuery = function( selector, context ) {
		return new jQuery.fn.init( selector, context );
	}
  init = jQuery.fn.init = function( selector, context, root ) {
		var match, elem;
		if ( !selector ) {
			return this;
		}
		root = root || rootjQuery;
		if ( typeof selector === "string" ) {
			if ( selector.charAt( 0 ) === "<" &&
				selector.charAt( selector.length - 1 ) === ">" &&
				selector.length >= 3 ) {
				match = [ null, selector, null ];

			} else {
				match = rquickExpr.exec( selector );
			}
			if ( match && ( match[ 1 ] || !context ) ) {
				if ( match[ 1 ] ) {
					context = context instanceof jQuery ? context[ 0 ] : context;
					jQuery.merge( this, jQuery.parseHTML(
						match[ 1 ],
						context && context.nodeType ? context.ownerDocument || context : document,
						true
					) );
					if ( rsingleTag.test( match[ 1 ] ) && jQuery.isPlainObject( context ) ) {
						for ( match in context ) {
							if ( jQuery.isFunction( this[ match ] ) ) {
								this[ match ]( context[ match ] );
							} else {
								this.attr( match, context[ match ] );
							}
						}
					}
					return this;

				} else {
					elem = document.getElementById( match[ 2 ] );
					if ( elem && elem.parentNode ) {
						if ( elem.id !== match[ 2 ] ) {
							return rootjQuery.find( selector );
						}
						this.length = 1;
						this[ 0 ] = elem;
					}
					this.context = document;
					this.selector = selector;
					return this;
				}
			} else if ( !context || context.jquery ) {
				return ( context || root ).find( selector );
			} else {
				return this.constructor( context ).find( selector );
			}
		} else if ( selector.nodeType ) {
			this.context = this[ 0 ] = selector;
			this.length = 1;
			return this;
		} else if ( jQuery.isFunction( selector ) ) {
			return typeof root.ready !== "undefined" ?
				root.ready( selector ) :
				selector( jQuery );
		}
		if ( selector.selector !== undefined ) {
			this.selector = selector.selector;
			this.context = selector.context;
		}
		return jQuery.makeArray( selector, this );
	};
```
