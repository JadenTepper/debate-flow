<script lang="ts">
	export let name: string;
	export let size: string = '1rem';
	let icons: { name: string; svg: string }[] = [
		{
			name: 'dots',
			svg: `<circle cx="26.25" cy="50.25" r="5.625" stroke-width="11.25"/>
<circle cx="71.25" cy="80.25" r="5.625" stroke-width="11.25"/>
<circle cx="71.25" cy="20.25" r="5.625" stroke-width="11.25"/>`
		},
		{
			name: 'arrowRight',
			svg: `<path d="M27 7L74 50L27 93" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>`
		},
		{
			name: 'arrowLeft',
			svg: `<path d="M74 93L27 50L74 7" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>`
		},
		{
			name: 'arrowUp',
			svg: `<path d="M7.5 73.5L50.5 26.5L93.5 73.5" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>`
		},
		{
			name: 'arrowDown',
			svg: `<path d="M93.5 26.5L50.5 73.5L7.5 26.5" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>`
		},
		{
			name: 'delete',
			svg: `<path d="M78.5685 22L22 78.5685" stroke-width="10" stroke-linecap="round"/>
<path d="M22 22L78.5685 78.5685" stroke-width="10" stroke-linecap="round"/>`
		},
		{
			name: 'add',
			svg: `<path d="M50 15L50 85" stroke-width="10" stroke-linecap="round"/>
<path d="M15 50H85" stroke-width="10" stroke-linecap="round"/>`
		},
		{
			name: 'download',
			svg: `<path d="M71 45L50 68L29 45" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M20 85L80 85" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M50 66L50 14" stroke-width="10" stroke-linecap="round"/>`
		},
		{
			name: 'upload',
			svg: `<path d="M29 37L50 14L71 37" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M20 85L80 85" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M50 16L50 68" stroke-width="10" stroke-linecap="round"/>`
		},
		{
			name: 'addUp',
			svg: `<path d="M85 25V25C87.7614 25 90 27.2386 90 30V70C90 75.5228 85.5228 80 80 80H20C14.4772 80 10 75.5228 10 70L10 30C10 27.2386 12.2386 25 15 25V25" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M35 25H65" stroke-width="10" stroke-linecap="round"/>
<path d="M50 40V10" stroke-width="10" stroke-linecap="round"/>`
		},
		{
			name: 'addDown',
			svg: `<path d="M15 75V75C12.2386 75 10 72.7614 10 70L10 30C10 24.4772 14.4772 20 20 20L80 20C85.5228 20 90 24.4772 90 30L90 70C90 72.7614 87.7614 75 85 75V75" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M65 75H35" stroke-width="10" stroke-linecap="round"/>
<path d="M50 60L50 90" stroke-width="10" stroke-linecap="round"/>`
		},
		{
			name: 'addRight',
			svg: `<path d="M75 85V85C75 87.7614 72.7614 90 70 90H30C24.4772 90 20 85.5228 20 80V20C20 14.4772 24.4772 10 30 10H70C72.7614 10 75 12.2386 75 15V15" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M75 35V65" stroke-width="10" stroke-linecap="round"/>
<path d="M60 50H90" stroke-width="10" stroke-linecap="round"/>`
		},
		{
			name: 'undo',
			svg: `<path d="M10 47H70C81.0457 47 90 55.9543 90 67V77" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M36 70L10 47L36 24" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>`
		},
		{
			name: 'redo',
			svg: `<path d="M90 47H30C18.9543 47 10 55.9543 10 67V77" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M64 70L90 47L64 24" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>`
		},
		{
			name: 'settings',
			svg: `<line x1="10" y1="50" x2="90" y2="50" stroke-width="10" stroke-linecap="round"/>
<line x1="10" y1="80" x2="90" y2="80" stroke-width="10" stroke-linecap="round"/>
<line x1="10" y1="20" x2="90" y2="20" stroke-width="10" stroke-linecap="round"/>
<circle cx="26.25" cy="50.25" r="6.25" stroke-width="10"/>
<circle cx="71.25" cy="80.25" r="6.25" stroke-width="10"/>
<circle cx="71.25" cy="20.25" r="6.25" stroke-width="10"/>`
		},
		{
			name: 'check',
			svg: `<path d="M88.7817 29.2843L39.2842 78.7817L11 50.4975" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>`
		},
		{
			name: 'home',
			svg: `<path d="M6 47L50 8L94 47" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M21 60L21 83C21 88.5228 25.4772 93 31 93H70C75.5228 93 80 88.5228 80 83V60" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>`
		},
		{
			name: 'cross',
			svg: `<path d="M10 50L90 50" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M50.566 50C36.9986 50 26 41.0457 26 30C26 18.9543 36.9986 10 50.566 10C57.3819 10 63.5495 12.2599 68 15.9095" stroke-width="10" stroke-linecap="round"/>
<path d="M49.434 50C63.0014 50 74 58.9543 74 70C74 81.0457 63.0014 90 49.434 90C42.6181 90 36.4505 87.7401 32 84.0905" stroke-width="10" stroke-linecap="round"/>`
		},
		{
			name: 'trash',
			svg: `
			<path d="M20 36L24.1594 80.922C24.6357 86.0656 28.9512 90 34.1168 90H65.8832C71.0488 90 75.3643 86.0656 75.8406 80.922L80 36L20 36Z" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M20 17L80 17" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M45 10V17H55V10H45Z" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>`
		},
		{
			name: 'arrowRoundLeft',
			svg: `<path d="M58.7626 38.862L51.5808 28.1397L44.399 17.4173L67.5606 6.02743" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M51.5 20C71.1061 20 87 35.8939 87 55.5C87 75.1061 71.1061 91 51.5 91C31.8939 91 16 75.1061 16 55.5C16 49.3035 17.5876 43.4778 20.3783 38.4074" stroke-width="10" stroke-linecap="round"/>
			`
		},
		{
			name: 'gear',
			svg: `<path d="M91.2583 35.059L96.0136 33.5139L96.0136 33.5139L91.2583 35.059ZM78.6576 28.6386L77.1125 23.8833L77.1125 23.8833L78.6576 28.6386ZM93.6849 42.5272L98.4402 40.9822L98.4402 40.9822L93.6849 42.5272ZM87.2645 55.128L85.7194 50.3727L85.7194 50.3727L87.2645 55.128ZM82.3777 56.7158L80.8326 51.9605L77.7668 52.9567L77.4086 56.1603L82.3777 56.7158ZM78.7743 68.354L74.3612 66.0035L72.8914 68.7633L74.7292 71.2929L78.7743 68.354ZM81.6715 72.3416L85.7166 69.4026L85.7166 69.4026L81.6715 72.3416ZM79.4592 86.3096L76.5203 82.2645L76.5202 82.2645L79.4592 86.3096ZM73.1063 90.9252L76.0452 94.9703L76.0452 94.9703L73.1063 90.9252ZM59.1382 88.7129L55.0932 91.6518L55.0932 91.6519L59.1382 88.7129ZM56.4461 85.0075L60.4912 82.0686L58.6057 79.4734L55.4608 80.1055L56.4461 85.0075ZM43.7058 85.0422L44.6641 80.1349L41.5348 79.5238L39.6607 82.1033L43.7058 85.0422ZM41.0388 88.7129L45.0839 91.6519L45.0839 91.6519L41.0388 88.7129ZM27.0708 90.9252L30.0097 86.8802L30.0097 86.8802L27.0708 90.9252ZM20.7179 86.3096L23.6568 82.2645L23.6568 82.2645L20.7179 86.3096ZM18.5056 72.3416L14.4605 69.4026L14.4605 69.4026L18.5056 72.3416ZM21.2875 68.5126L25.3326 71.4515L27.1818 68.9063L25.6875 66.1378L21.2875 68.5126ZM17.5916 56.6483L22.5618 56.1032L22.2095 52.8915L19.1367 51.893L17.5916 56.6483ZM12.9125 55.128L11.3675 59.8833L11.3675 59.8833L12.9125 55.128ZM6.49215 42.5273L11.2474 44.0723L11.2474 44.0723L6.49215 42.5273ZM8.91874 35.059L4.16346 33.5139L4.16346 33.5139L8.91874 35.059ZM21.5195 28.6386L19.9744 33.3939L19.9744 33.3939L21.5195 28.6386ZM26.6486 30.3051L25.1035 35.0604L28.0594 36.0208L30.2289 33.7954L26.6486 30.3051ZM36.1622 23.5313L38.2858 28.058L41.1622 26.7085V23.5313L36.1622 23.5313ZM64.0148 23.6261H59.0148V26.7794L61.8604 28.1381L64.0148 23.6261ZM73.3763 30.3546L69.7887 33.8373L71.9586 36.0725L74.9214 35.1098L73.3763 30.3546ZM96.0136 33.5139C93.4536 25.6351 84.9913 21.3233 77.1125 23.8833L80.2027 33.3938C82.8289 32.5405 85.6497 33.9778 86.503 36.604L96.0136 33.5139ZM98.4402 40.9822L96.0136 33.5139L86.503 36.604L88.9296 44.0723L98.4402 40.9822ZM88.8096 59.8833C96.6884 57.3233 101 48.861 98.4402 40.9822L88.9296 44.0723C89.7829 46.6986 88.3457 49.5194 85.7194 50.3727L88.8096 59.8833ZM83.9228 61.4711L88.8096 59.8833L85.7194 50.3727L80.8326 51.9605L83.9228 61.4711ZM77.4086 56.1603C77.0145 59.6866 75.9562 63.0088 74.3612 66.0035L83.1874 70.7044C85.3641 66.6174 86.8092 62.0798 87.3467 57.2713L77.4086 56.1603ZM85.7166 69.4026L82.8194 65.415L74.7292 71.2929L77.6264 75.2805L85.7166 69.4026ZM82.3981 90.3547C89.1002 85.4853 90.586 76.1047 85.7166 69.4026L77.6264 75.2805C79.2495 77.5145 78.7543 80.6414 76.5203 82.2645L82.3981 90.3547ZM76.0452 94.9703L82.3981 90.3547L76.5202 82.2645L70.1673 86.8801L76.0452 94.9703ZM55.0932 91.6519C59.9625 98.354 69.3431 99.8397 76.0452 94.9703L70.1673 86.8801C67.9333 88.5033 64.8064 88.008 63.1833 85.774L55.0932 91.6519ZM52.401 87.9464L55.0932 91.6518L63.1833 85.774L60.4912 82.0686L52.401 87.9464ZM55.4608 80.1055C53.6961 80.4603 51.8666 80.6472 49.9884 80.6472V90.6472C52.532 90.6472 55.0215 90.3938 57.4314 89.9095L55.4608 80.1055ZM49.9884 80.6472C48.1626 80.6472 46.383 80.4705 44.6641 80.1349L42.7475 89.9495C45.0945 90.4078 47.5159 90.6472 49.9884 90.6472V80.6472ZM45.0839 91.6519L47.7509 87.9811L39.6607 82.1033L36.9937 85.774L45.0839 91.6519ZM24.1319 94.9703C30.834 99.8397 40.2145 98.354 45.0839 91.6519L36.9937 85.774C35.3706 88.008 32.2438 88.5033 30.0097 86.8802L24.1319 94.9703ZM17.779 90.3547L24.1319 94.9703L30.0097 86.8802L23.6568 82.2645L17.779 90.3547ZM14.4605 69.4026C9.59111 76.1048 11.0769 85.4853 17.779 90.3547L23.6568 82.2645C21.4228 80.6414 20.9275 77.5145 22.5507 75.2805L14.4605 69.4026ZM17.2424 65.5736L14.4605 69.4026L22.5507 75.2805L25.3326 71.4515L17.2424 65.5736ZM25.6875 66.1378C24.0437 63.092 22.9567 59.7034 22.5618 56.1032L12.6214 57.1935C13.1599 62.1028 14.6442 66.7311 16.8875 70.8874L25.6875 66.1378ZM11.3675 59.8833L16.0465 61.4036L19.1367 51.893L14.4576 50.3727L11.3675 59.8833ZM1.73687 40.9822C-0.823121 48.861 3.48865 57.3233 11.3675 59.8833L14.4576 50.3727C11.8314 49.5194 10.3941 46.6986 11.2474 44.0723L1.73687 40.9822ZM4.16346 33.5139L1.73687 40.9822L11.2474 44.0723L13.674 36.6041L4.16346 33.5139ZM23.0646 23.8833C15.1857 21.3233 6.72344 25.6351 4.16346 33.5139L13.674 36.6041C14.5274 33.9778 17.3481 32.5405 19.9744 33.3939L23.0646 23.8833ZM28.1937 25.5498L23.0646 23.8833L19.9744 33.3939L25.1035 35.0604L28.1937 25.5498ZM30.2289 33.7954C32.5366 31.4281 35.2634 29.4758 38.2858 28.058L34.0386 19.0047C29.9154 20.939 26.2046 23.5978 23.0684 26.8149L30.2289 33.7954ZM31.1622 18V23.5313L41.1622 23.5313V18L31.1622 18ZM46.1622 3C37.8779 3 31.1622 9.71573 31.1622 18L41.1622 18C41.1622 15.2386 43.4008 13 46.1622 13V3ZM54.0148 3L46.1622 3V13L54.0148 13V3ZM69.0148 18C69.0148 9.71572 62.2991 3 54.0148 3V13C56.7762 13 59.0148 15.2386 59.0148 18H69.0148ZM69.0148 23.6261V18H59.0148V23.6261H69.0148ZM61.8604 28.1381C64.8331 29.5575 67.5155 31.4956 69.7887 33.8373L76.9639 26.8719C73.8745 23.6894 70.2243 21.0503 66.1692 19.114L61.8604 28.1381ZM77.1125 23.8833L71.8312 25.5993L74.9214 35.1098L80.2027 33.3938L77.1125 23.8833Z" fill="currentColor"/>
<circle cx="50.25" cy="53.25" r="5.625" stroke-width="11.25"/>
`
		},
		{
			name: 'ellipses',
			svg: `<circle cx="19.25" cy="50.25" r="5.625" stroke-width="11.25"/>
<circle cx="50.25" cy="50.25" r="5.625" stroke-width="11.25"/>
<circle cx="81.25" cy="50.25" r="5.625" stroke-width="11.25"/>`
		},
		{
			name: 'link',
			svg: `<path d="M42.9289 71.2132L53.5355 81.8198C61.346 89.6303 74.0093 89.6303 81.8198 81.8198V81.8198C89.6303 74.0093 89.6303 61.346 81.8198 53.5355L71.2132 42.9289" stroke-width="10" stroke-linecap="round"/>
<path d="M28.7868 57.0711L18.1802 46.4645C10.3697 38.654 10.3697 25.9907 18.1802 18.1802V18.1802C25.9907 10.3697 38.654 10.3697 46.4645 18.1802L57.0711 28.7868" stroke-width="10" stroke-linecap="round"/>
<path d="M37.2721 37.2721L63.0815 63.0815" stroke-width="10" stroke-linecap="round"/>`
		},
		{
			name: 'copy',
			svg: `<path d="M20 73V73C17.2386 73 15 70.7614 15 68L15 19C15 13.4772 19.4772 9 25 9H60C62.7614 9 65 11.2386 65 14V14" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M35 38V82C35 87.5228 39.4772 92 45 92H75C80.5228 92 85 87.5228 85 82V38C85 32.4772 80.5228 28 75 28H45C39.4772 28 35 32.4772 35 38Z" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>`
		},
		{
			name: 'file',
			svg: `<path d="M17 20L17 80C17 85.5228 21.4772 90 27 90H72C77.5228 90 82 85.5228 82 80V35L57 10H27C21.4772 10 17 14.4771 17 20Z" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M52 10V40H82" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>`
		},
		{
			name: 'people',
			svg: `<circle cx="21" cy="21" r="21" transform="matrix(-1 0 0 1 80.6039 16.1776)" stroke-width="10"/>
<path fill="currentColor" d="M49.5683 55.1775L52.0719 50.8495L59.5538 55.1775L52.0719 59.5055L49.5683 55.1775ZM49.5683 18.8085L52.0719 14.4805L59.5538 18.8085L52.0719 23.1365L49.5683 18.8085ZM44.0718 36.993C44.0718 42.9064 47.2786 48.0766 52.0719 50.8495L47.0647 59.5055C39.3084 55.0187 34.0718 46.6204 34.0718 36.993H44.0718ZM52.0719 23.1365C47.2786 25.9093 44.0718 31.0796 44.0718 36.993H34.0718C34.0718 27.3656 39.3084 18.9672 47.0647 14.4805L52.0719 23.1365ZM47.0647 23.1365C44.7174 21.7787 41.9931 21 39.0718 21V11C43.798 11 48.2436 12.2659 52.0719 14.4805L47.0647 23.1365ZM39.0718 21C30.2391 21 23.0788 28.1603 23.0788 36.993H13.0788C13.0788 22.6375 24.7163 11 39.0718 11V21ZM23.0788 36.993C23.0788 45.8257 30.2391 52.986 39.0718 52.986V62.986C24.7163 62.986 13.0788 51.3485 13.0788 36.993H23.0788ZM39.0718 52.986C41.9931 52.986 44.7174 52.2073 47.0647 50.8495L52.0719 59.5055C48.2436 61.7201 43.798 62.986 39.0718 62.986V52.986Z" />
<path d="M92.6039 83.1776C92.6039 49.8442 28.6039 49.8442 28.6039 83.1776" stroke-width="10" stroke-linecap="round" />
<path d="M51.2842 54.3741C53.9662 55.0319 55.607 57.7393 54.9492 60.4213C54.2914 63.1032 51.584 64.7441 48.902 64.0862L51.2842 54.3741ZM12.5823 83.1775C12.5823 85.939 10.3438 88.1775 7.58235 88.1775C4.82092 88.1775 2.58235 85.939 2.58235 83.1775H12.5823ZM48.902 64.0862C40.6164 62.0539 31.1881 62.8609 24.0296 66.302C17.0403 69.6618 12.5823 75.2606 12.5823 83.1775H2.58235C2.58235 70.5678 10.0806 61.912 19.6972 57.2893C29.1445 52.7479 40.9716 51.8446 51.2842 54.3741L48.902 64.0862Z" fill="currentColor"/>`
		},
		{
			name: 'flower',
			svg: `
			<path d="M27 47L27 10C27 7.23858 29.2386 5 32 5L37 5" stroke-width="10" stroke-linecap="round"/>
<path d="M41.7512 22.4399L76.7795 11.0585C79.4058 10.2052 82.2265 11.6424 83.0799 14.2687L84.7664 19.4593" stroke-width="10" stroke-linecap="round"/>
<path d="M69.9781 32.0025L91.6268 61.7993C93.2499 64.0333 92.7547 67.1602 90.5206 68.7833L86.1052 71.9913" stroke-width="10" stroke-linecap="round"/>
<path d="M68.5615 60.1581L46.9128 89.9549C45.2897 92.189 42.1629 92.6842 39.9288 91.0611L35.5134 87.8531" stroke-width="10" stroke-linecap="round"/>
<path d="M44.7835 68.5174L9.75526 57.136C7.12899 56.2827 5.69174 53.4619 6.54506 50.8356L8.23159 45.645" stroke-width="10" stroke-linecap="round"/>
<path d="M74 45C74 58.3372 63.3971 69 50.5 69C37.6029 69 27 58.3372 27 45C27 31.6628 37.6029 21 50.5 21C63.3971 21 74 31.6628 74 45Z" stroke-width="10"/>
<path d="M74 45C74 58.3372 63.3971 69 50.5 69C37.6029 69 27 58.3372 27 45C27 31.6628 37.6029 21 50.5 21C63.3971 21 74 31.6628 74 45Z" stroke-width="10"/>`
		},
		{
			name: 'eye',
			svg: `
			<path d="M49.5 16C70.2642 16 87.7516 30.1877 93 49.5C87.7516 68.8123 70.2642 83 49.5 83C28.7358 83 11.2484 68.8123 6 49.5C11.2484 30.1877 28.7358 16 49.5 16Z" stroke-width="10"/>
<circle cx="50" cy="50" r="15" stroke-width="10"/>`
		},
		{
			name: 'pause',
			svg: `
			<path d="M18 23L18 76C18 81.5228 22.4772 86 28 86C33.5228 86 38 81.5228 38 76V23C38 17.4771 33.5228 13 28 13C22.4772 13 18 17.4771 18 23Z" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M61 23L61 76C61 81.5228 65.4772 86 71 86C76.5228 86 81 81.5228 81 76V23C81 17.4771 76.5228 13 71 13C65.4772 13 61 17.4771 61 23Z" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>`
		},
		{
			name: 'play',
			svg: `
			<path d="M85 41.3398C91.6667 45.1888 91.6667 54.8113 85 58.6603L34 88.1051C27.3333 91.9541 19 87.1429 19 79.4449L19 20.5551C19 12.8571 27.3333 8.04589 34 11.8949L85 41.3398Z" stroke-width="10"/>
			`
		},
		{
			name: 'clock',
			svg: `
			<circle cx="50" cy="50" r="45" stroke-width="10"/>
<path d="M33 40L50.3205 50" stroke-width="10" stroke-linecap="round"/>
<path d="M50 5V15" stroke-width="10" stroke-linecap="round"/>
<path d="M50 85V95" stroke-width="10" stroke-linecap="round"/>
<path d="M85 50L95 50" stroke-width="10" stroke-linecap="round"/>
<path d="M5 50L15 50" stroke-width="10" stroke-linecap="round"/>
<path d="M71.2132 29L50 50.2132" stroke-width="10" stroke-linecap="round"/>
			`
		},
		{
			name: 'angleBrackets',
			svg: `
			<path d="M27 69L6 50L27 31" stroke="currentColor" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M72 31L93 50L72 69" stroke="currentColor" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M42 78.9556L57.5291 21" stroke="currentColor" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
			`
		},
		{
			name: 'delta',
			svg: `
<path d="M54.3301 24.5L80.3109 69.5C82.2354 72.8333 79.8298 77 75.9808 77H24.0192C20.1702 77 17.7646 72.8333 19.6891 69.5L45.6699 24.5C47.5944 21.1667 52.4056 21.1667 54.3301 24.5Z" stroke="currentColor" stroke-width="10"/>
			`
		},
		{
			name: 'letterB',
			svg: `
			<path d="M58 10H32C29.7909 10 28 11.7909 28 14V45C28 47.7614 30.2386 50 33 50H58C69.0457 50 78 41.0457 78 30C78 18.9543 69.0457 10 58 10Z" stroke="currentColor" stroke-width="10"/>
<path d="M58 50H28V85C28 87.7614 30.2386 90 33 90H58C69.0457 90 78 81.0457 78 70C78 58.9543 69.0457 50 58 50Z" stroke="currentColor" stroke-width="10"/>
			`
		},
		{
			name: 'open',
			svg: `
					<path d="M62 10.8492L90.2843 9.43503L88.8701 37.7193" stroke="currentColor" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
					<path d="M89.7696 10L53 46.7696" stroke="currentColor" stroke-width="10" stroke-linecap="round"/>
					<path d="M90 61V80C90 85.5228 85.5228 90 80 90H20C14.4772 90 10 85.5228 10 80V20C10 14.4772 14.4772 10 20 10H39" stroke="currentColor" stroke-width="10" stroke-linecap="round"/>
					`
		},
		{
			name: 'addPerson',
			svg: `<path d="M17 35V65" stroke="currentColor" stroke-width="10" stroke-linecap="round"/>
			<path d="M2 50H32" stroke="currentColor" stroke-width="10" stroke-linecap="round"/>
			<circle cx="21" cy="21" r="21" transform="matrix(-1 0 0 1 88 16)" stroke="currentColor" stroke-width="10"/>
			<path d="M100 83C100 49.6667 36 49.6667 36 83" stroke="currentColor" stroke-width="10" stroke-linecap="round"/>`
		},
		{
			name: 'unfoldArrows',
			svg: `<path d="M30 29L49 8L68 29" stroke="currentColor" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M68 71L49 92L30 71" stroke="currentColor" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>`
		},
		{
			name: 'foldArrows',
			svg: `<path d="M68 8L49 29L30 8" stroke="currentColor" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M30 92L49 71L68 92" stroke="currentColor" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>`
		},
		{
			name: 'arrowRightThroughCircle',
			svg: `<line x1="5" y1="50" x2="25" y2="50" stroke="currentColor" stroke-width="10" stroke-linecap="round"/>
<line x1="55" y1="50" x2="90" y2="50" stroke="currentColor" stroke-width="10" stroke-linecap="round"/>
<path d="M69 73L95 50L69 27" stroke="currentColor" stroke-width="10" stroke-linecap="round" stroke-linejoin="round"/>
<path d="M37.5 62C44.4036 62 50 56.4036 50 49.5C50 42.5964 44.4036 37 37.5 37C30.5964 37 25 42.5964 25 49.5C25 56.4036 30.5964 62 37.5 62Z" stroke="currentColor" stroke-width="10"/>`
		}
	];
	let displayIcon: { name: string; svg: string } | null;
	function findIcon() {
		displayIcon = icons.find((icon: { name: string; svg: string }) => icon.name === name) ?? null;
	}
	findIcon();
	$: name, findIcon();
</script>

<svg
	style={`width:${size};height:${size};`}
	viewBox="0 0 {100} {100}"
	fill="none"
	stroke="var(--text)"
>
	{@html displayIcon?.svg ?? icons[0].svg}
</svg>

<style>
	svg {
		display: block;
		margin: auto;
		stroke: currentColor;
	}
</style>
