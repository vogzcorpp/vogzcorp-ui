# SocialProofCompanies Components by Vogzcorp

Just copy past the code below to add the component source code:

```js
import clsx from 'clsx';
import Image from 'next/image';
import React from 'react';

const SocialProofCompanies = ({
	elems,
	type,
	dark = 'from-zinc-900',
	light = 'from-white',
}: {
	elems: {
		label?: string,
		logo?: string,
	}[],
	type: 'toggle' | 'dark' | 'light' | 'default',
	dark?: string,
	light?: string,
}) => {
	const toogleState =
		type == 'toggle'
			? `from-${light} dark:from-${dark}`
			: type == 'dark'
			? `from-${dark}`
			: type == 'light'
			? `from-${light}`
			: type == 'default'
			? 'from-white dark:from-zinc-900'
			: '';

	const Comp = () => {
		return (
			<div className="flex shrink-0 justify-around items-center [gap:var(--gap)] animate-marquee flex-row">
				{elems.map(items => {
					return (
						<Image
							src={items.logo ?? ''}
							alt={items.label ?? ''}
							width={100}
							height={0}
							className="h-max w-28 dark:brightness-0 dark:invert"
							key={items.label}
						/>
					);
				})}
			</div>
		);
	};

	return (
		<div className="relative mt-6 max-w-[800px]">
			<div className="group flex overflow-hidden p-2 [--gap:3rem] [gap:var(--gap)] flex-row max-w-full [--duration:30s]">
				<Comp />
				<Comp />
				<Comp />
				<Comp />
			</div>
			<div
				className={clsx(
					'pointer-events-none absolute inset-y-0 left-0 h-full w-1/3 bg-gradient-to-r',
					toogleState,
				)}
			></div>
			<div
				className={clsx(
					'pointer-events-none absolute inset-y-0 right-0 h-full w-1/3 bg-gradient-to-l',
					toogleState,
				)}
			></div>
		</div>
	);
};

export default SocialProofCompanies;
```

And now, use it

Check the [tailwind color panel](https://tailwindcss.com/docs/customizing-colors) to specify the correct color

```js
import SocialProofCompanies from '@/component/ui/SocialProofCompanies';

function App() {
	return (
          // #### RECOMMENDED ####
          <SocialProofCompanies
            elems={array}
            type="toogle"
            light="white"
            dark="black"
          />
          // Supports dark and light mode but you need to specify "light" and "dark" args

          ///#####################################################################
          ///###########################OTHER SETTINGS############################
          ///#####################################################################

          <SocialProofCompanies
            elems={array}
            type="dark"
            dark="black"
          />
          // Supports dark mode but you need to specify "dark" arg


          <SocialProofCompanies
            elems={array}
            type="light"
            light="white"
          />
          // Supports light mode but you need to specify "light" arg


          <SocialProofCompanies
            elems={array}
            type="default"
          />
          // Supports dark and light modes, but you don't need to specify a custom color
	);
}

const array = [
	{
		name: 'vogzcorp',
		logo: '/vogzcorp.svg', // return the file from public folder (nextjs)
	},
    {
		name: 'google',
		logo: '/google.svg', // return the file from public folder (nextjs)
	},
    {
		name: 'apple',
		logo: 'https://upload.wikimedia.org/wikipedia/commons/thumb/f/fa/Apple_logo_black.svg/814px-Apple_logo_black.svg.png',
        // You can also specify links
	},
];
```
