# WAI-ARIA WordPress Walker

Custom nav menu walker that outputs ARIA attributes for a navigation with flyout submenus. Code builds upon the [WAI-ARIA WordPress Walker](https://github.com/proteusthemes/WAI-ARIA-Walker_Nav_Menu) done by [primozcigler](https://github.com/primozcigler).

The walker outputs the recommended accessibility design pattern for [flyout menus](https://www.w3.org/WAI/tutorials/menus/flyout/) and [navigation menu buttons](https://www.w3.org/TR/wai-aria-practices/examples/menu-button/menu-button-links.html) from [w3.org](https://www.w3.org/). 

See [my demo here](https://codepen.io/michow/pen/Koojpp).

## Usage

1. Copy the code from `aria-walker-flyout-menu.php` into `/<path-to-wp>/wp-content/themes/<theme-name>/functions.php`
2. Instantiate `Aria_Walker_Flyout_Menu` and pass it as an argument to `wp_nav_menu()` through the `wp_nav_menu` array

		<nav class="your-class" aria-label="Main Menu">
			<?php
				wp_nav_menu( array(
					'theme_location' => 'your_menu_name_here',
					'depth'          => 2,
					'container'      => false,
					'menu_class'     => 'menu-top-nav',
					'walker'         => new Aria_Walker_Flyout_Menu(),
					'items_wrap'     => '<ul id="%1$s" class="%2$s">%3$s</ul>'
				) );
			?>
		</nav>
	  
> **Note:** You will need to include the appropriate js and css to toggle ARIA attributes and control the button. View my demo for example code.

## Sample Output
 
For any parent link that has a submenu, it will render a `button` with its `aria-controls` value matching the `id` of the submenu it triggers. It will also output the necessary `aria-haspopup` and `aria-expanded` attributes.
 
		<nav class="your-class" aria-label="Main Menu">
			<ul id="menu-top-nav" class="menu-top-nav" role="menubar">
				<li id="menu-item-111" class="menu-item menu-item-has-children...">
					<a href="#" role="menuitem" aria-haspopup="true" aria-expanded="false">List 1</a>
					<button aria-expanded="false" aria-controls="submenu-111">
						<span class="sr-only">Toggle submenu</span>
					</button>
					<ul role="menu" class="sub-menu" id="submenu-111">
						<li id="menu-item-112" class="menu-item...">
							<a href="#" role="menuitem">List 1 Item 1</a>
						</li>
						<li id="menu-item-113" class="menu-item...">
							<a href="#" role="menuitem">List 1 Item 2</a>
						</li>
					</ul>
				</li>
				<li id="menu-item-679" class="menu-item menu-item-211">
					<a href="#" role="menuitem">List 2</a>
				</li>
			</ul>
		</nav>