<style>
	header {
		position: relative;
		text-align: center;
		font-size: 2em;
		z-index: 1;
		color: #f5f5f5;
		text-shadow: 0px 0px 6px #008f3b;
		padding-bottom: 2em;
	}

	header::before {
		position: absolute;
		content: '';
		width: 200vw;
		height: 500%;
		background:#00e676;
		border-radius: 50%;
		bottom: 1em;
		left: 50%;
		transform: translateX(-50%);
		z-index: -1;
	}

	#cost {
		text-align: center;
		font-family: 'Space Mono', monospace;
		font-size: 48px;
		color: #00e676;
		text-shadow: 0px 0px 0px #455a64, 0px 1px 0px #455a64, 1px 0px 0px #455a64, 1px 1px 0px #455a64;
		font-weight: 900;
	}

	label {
		display: flex;
		justify-content: space-between;
		margin-top: 5px;
		padding-top: 10px;
		font-size: 18px;
		border-top: solid 1px #bdbdbd;
	}

	label:first-child {
		border-top: none;
	}

	.description {
		border-top: solid 1px #bdbdbd;
		margin-top: 5px;
		padding-top: 15px;
		font-size: 18px;
	}
</style>

<script>
	import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';
	
	const CPI_2017_MAP = new Map([[1774,0.033],[1775,0.031],[1776,0.035],[1777,0.043],[1778,0.056],[1779,0.050],[1780,0.056],[1781,0.045],[1782,0.049],[1783,0.043],[1784,0.042],[1785,0.040],[1786,0.039],[1787,0.038],[1788,0.036],[1789,0.036],[1790,0.038],[1791,0.038],[1792,0.039],[1793,0.040],[1794,0.045],[1795,0.051],[1796,0.054],[1797,0.052],[1798,0.050],[1799,0.050],[1800,0.051],[1801,0.052],[1802,0.044],[1803,0.046],[1804,0.048],[1805,0.048],[1806,0.050],[1807,0.047],[1808,0.051],[1809,0.050],[1810,0.050],[1811,0.053],[1812,0.054],[1813,0.065],[1814,0.063],[1815,0.058],[1816,0.054],[1817,0.052],[1818,0.052],[1819,0.048],[1820,0.046],[1821,0.048],[1822,0.043],[1823,0.040],[1824,0.040],[1825,0.040],[1826,0.041],[1827,0.039],[1828,0.038],[1829,0.038],[1830,0.035],[1831,0.035],[1832,0.034],[1833,0.035],[1834,0.036],[1835,0.038],[1836,0.039],[1837,0.038],[1838,0.038],[1839,0.035],[1840,0.035],[1841,0.033],[1842,0.030],[1843,0.031],[1844,0.031],[1845,0.031],[1846,0.033],[1847,0.032],[1848,0.031],[1849,0.032],[1850,0.031],[1851,0.031],[1852,0.031],[1853,0.031],[1854,0.034],[1855,0.035],[1856,0.035],[1857,0.035],[1858,0.033],[1859,0.034],[1860,0.034],[1861,0.036],[1862,0.041],[1863,0.051],[1864,0.064],[1865,0.066],[1866,0.065],[1867,0.060],[1868,0.058],[1869,0.055],[1870,0.053],[1871,0.050],[1872,0.050],[1873,0.049],[1874,0.047],[1875,0.045],[1876,0.044],[1877,0.043],[1878,0.041],[1879,0.041],[1880,0.042],[1881,0.042],[1882,0.042],[1883,0.041],[1884,0.040],[1885,0.040],[1886,0.038],[1887,0.039],[1888,0.039],[1889,0.038],[1890,0.037],[1891,0.037],[1892,0.037],[1893,0.037],[1894,0.035],[1895,0.034],[1896,0.034],[1897,0.034],[1898,0.034],[1899,0.034],[1900,0.034],[1901,0.035],[1902,0.035],[1903,0.036],[1904,0.036],[1905,0.036],[1906,0.037],[1907,0.038],[1908,0.038],[1909,0.037],[1910,0.039],[1911,0.039],[1912,0.040],[1913,0.040],[1914,0.041],[1915,0.041],[1916,0.044],[1917,0.052],[1918,0.062],[1919,0.071],[1920,0.082],[1921,0.073],[1922,0.069],[1923,0.070],[1924,0.070],[1925,0.071],[1926,0.072],[1927,0.071],[1928,0.070],[1929,0.070],[1930,0.068],[1931,0.062],[1932,0.056],[1933,0.053],[1934,0.055],[1935,0.056],[1936,0.057],[1937,0.059],[1938,0.058],[1939,0.057],[1940,0.057],[1941,0.060],[1942,0.066],[1943,0.071],[1944,0.072],[1945,0.073],[1946,0.080],[1947,0.091],[1948,0.098],[1949,0.097],[1950,0.098],[1951,0.106],[1952,0.108],[1953,0.109],[1954,0.110],[1955,0.109],[1956,0.111],[1957,0.115],[1958,0.118],[1959,0.119],[1960,0.121],[1961,0.122],[1962,0.123],[1963,0.125],[1964,0.126],[1965,0.129],[1966,0.132],[1967,0.136],[1968,0.142],[1969,0.150],[1970,0.158],[1971,0.165],[1972,0.171],[1973,0.181],[1974,0.201],[1975,0.219],[1976,0.232],[1977,0.247],[1978,0.266],[1979,0.296],[1980,0.336],[1981,0.371],[1982,0.394],[1983,0.406],[1984,0.424],[1985,0.439],[1986,0.447],[1987,0.463],[1988,0.483],[1989,0.506],[1990,0.533],[1991,0.556],[1992,0.572],[1993,0.590],[1994,0.605],[1995,0.622],[1996,0.640],[1997,0.655],[1998,0.665],[1999,0.680],[2000,0.703],[2001,0.723],[2002,0.734],[2003,0.751],[2004,0.771],[2005,0.797],[2006,0.822],[2007,0.846],[2008,0.878],[2009,0.875],[2010,0.890],[2011,0.918],[2012,0.937],[2013,0.950],[2014,0.966],[2015,0.967],[2016,0.979],[2017,1.000],[2018,1.025],[2019,1.043],[2020,1.052]]);

	let year = 1845;
	let boards = 1;
	let shingles = 1;
	let laths = 1;
	let windows = 2;
	let bricks = 1000;
	let limeCasks = 2;
	let hair = 1;
	let mantleTree = 1;
	let nails = 1;
	let hingesAndScrews = 1;
	let latch = 1;
	let chalk = 1;
	let transportation = 1;
	
	const tweenedCost = tweened(0, {
		duration: 500,
		easing: cubicOut
	})

	$: cost = () => {
		let bareCost = boards * 8.035 + shingles * 4 + laths * 1.25 + windows * 2.43 / 2 + bricks * 4 / 1000 + limeCasks * 2.40 / 2 + hair * .31 + mantleTree * .15 + nails * 3.90 + hingesAndScrews * .14 + latch * .1 + chalk * .01 + transportation * 1.4;
		let adjustedInflation = adjustInflation(bareCost);
		tweenedCost.set(adjustedInflation);		
	}

	$: adjustInflation = (bareCost) => {
		return bareCost * (CPI_2017_MAP.get(year) / CPI_2017_MAP.get(1845));
	}

	$: costPrettify = (cost) => {
		let centsArray = Math.round(cost * 100).toString().padStart(2, '0').split('');
		centsArray.splice(centsArray.length - 2, 0, '.')
		return '$' + centsArray.join('');
	}
</script>

<svelte:head>
	<title>The Cost of Walden</title>
</svelte:head>

<header>
	The Cost of Walden
</header>

<h1 id="cost" data-cents={cost()}>{costPrettify($tweenedCost)}</h1>

<datalist id="tickmarks">
	<option value="1845" />
</datalist>

<label for="year" style="border-top: none;"><div>Year: {year}</div></label>
<input id="year" type="range" min="1774" max="2020" bind:value={year} list="tickmarks">

<label for="boards"><div>Boards: {boards}x</div><div>{costPrettify(adjustInflation(boards * 8.035))}</div></label>
<input id="boards" type="range" min="0" max="10" bind:value={boards}>

<label for="shingles"><div>Refuse shingles: {shingles}x</div><div>{costPrettify(adjustInflation(shingles * 4))}</div></label>
<input id="shingles" type="range" min="0" max="10" bind:value={shingles}>

<label for="laths"><div>Laths: {laths}x</div><div>{costPrettify(adjustInflation(laths * 1.25))}</div></label>
<input id="laths" type="range" min="0" max="10" bind:value={laths}>

<label for="windows"><div>Windows: {windows}</div><div>{costPrettify(adjustInflation(windows * 2.43 / 2))}</div></label>
<input id="windows" type="range" min="0" max="10" bind:value={windows}>

<label for="bricks"><div>Bricks: {bricks}</div><div>{costPrettify(adjustInflation(bricks * 4 / 1000))}</div></label>
<input id="bricks" type="range" min="0" max="10000" step="100" bind:value={bricks}>

<label for="limeCasks"><div>Lime Casks: {limeCasks}</div><div>{costPrettify(adjustInflation(limeCasks * 2.40 / 2))}</div></label>
<input id="limeCasks" type="range" min="0" max="10" bind:value={limeCasks}>

<label for="hair"><div>Hair: {hair}x</div><div>{costPrettify(adjustInflation(hair * .31))}</div></label>
<input id="hair" type="range" min="0" max="10" bind:value={hair}>

<label for="mantleTree"><div>Mantle-tree iron: {mantleTree}</div><div>{costPrettify(adjustInflation(mantleTree * .15))}</div></label>
<input id="mantleTree" type="range" min="0" max="10" bind:value={mantleTree}>

<label for="nails"><div>Nails: {nails}x</div><div>{costPrettify(adjustInflation(nails * 3.90))}</div></label>
<input id="nails" type="range" min="0" max="10" bind:value={nails}>

<label for="hingesAndScrews"><div>Hinges and Screws: {hingesAndScrews}x</div><div>{costPrettify(adjustInflation(hingesAndScrews * .14))}</div></label>
<input id="hingesAndScrews" type="range" min="0" max="10" bind:value={hingesAndScrews}>

<label for="latch"><div>Latch: {latch}</div><div>{costPrettify(adjustInflation(latch * .1))}</div></label>
<input id="latch" type="range" min="0" max="10" bind:value={latch}>

<label for="chalk"><div>Chalk: {chalk}x</div><div>{costPrettify(adjustInflation(chalk * .01))}</div></label>
<input id="chalk" type="range" min="0" max="10" bind:value={chalk}>

<label for="transportation"><div>Transportation: {transportation ? 'Yes': 'No'}</div><div>{costPrettify(adjustInflation(transportation * 1.4))}</div></label>
<input id="transportation" type="range" min="0" max="1" bind:value={transportation}>

<div class="description">
	<h1>
		About
	</h1>
	This tool offers a simple way to see how much it would've roughly cost to live at Walden pond based on Thoreau's list of materials he had in his chapter <i>Economy</i>. You can also play around with quantities, if say, you wanted to have four windows instead of two! See how much your cabin on Walden pond would cost.
	<br>
	<br>
	The prices adjusted for inflation are calculated using the CPIs calculated by Robert Sahr of Oregon State University, which can be found <a href="https://liberalarts.oregonstate.edu/spp/polisci/research/inflation-conversion-factors-convert-dollars-1774-estimated-2024-dollars-recent-year">here</a>.
</div>
