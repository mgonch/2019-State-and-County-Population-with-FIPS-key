# 2019-State-and-County-Population-with-FIPS-key

{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Julia Functions to Access State and County Populations based upon 2019 Cenus Data"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "I developed these while analyzing COVID-19 data. I wanted to be able to use the FIPS number (a US Census terms), a field in the New York Times (https://github.com/nytimes/covid-19-data) COVID-19 database, as a key to augment their data with State and County populations."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Accesor API to get Populations"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Copy and Paste these self contained Julia functions into code (No Packages needed)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### State Populations"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 45,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "get_state_populations (generic function with 1 method)"
      ]
     },
     "execution_count": 45,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "using CSV\n",
    "function get_state_populations()\n",
    "    CSV.read(\"2019_state_populations.csv\",type=String,types=Dict(3=>Int64))\n",
    "end"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### County Populations"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 49,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "get_county_populations (generic function with 1 method)"
      ]
     },
     "execution_count": 49,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "using CSV\n",
    "function get_county_populations()\n",
    "    CSV.read(\"2019_county_populations.csv\",type=String,types=Dict(4=>Int64))\n",
    "end"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Documenting development of these functions"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [],
   "source": [
    "using CSV, DataFrames"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "\"https://www2.census.gov/programs-surveys/popest/datasets/2010-2019/counties/totals/co-est2019-alldata.csv\""
      ]
     },
     "execution_count": 2,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "url = \"https://www2.census.gov/programs-surveys/popest/datasets/2010-2019/counties/totals/co-est2019-alldata.csv\""
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "\"us_census.csv\""
      ]
     },
     "execution_count": 3,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "download(url,\"us_census.csv\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table class=\"data-frame\"><thead><tr><th></th><th>SUMLEV</th><th>REGION</th><th>DIVISION</th><th>STATE</th><th>COUNTY</th><th>STNAME</th><th>CTYNAME</th><th>CENSUS2010POP</th></tr><tr><th></th><th>String</th><th>String</th><th>String</th><th>String</th><th>String</th><th>String</th><th>String</th><th>String</th></tr></thead><tbody><p>5 rows × 164 columns (omitted printing of 156 columns)</p><tr><th>1</th><td>040</td><td>3</td><td>6</td><td>01</td><td>000</td><td>Alabama</td><td>Alabama</td><td>4779736</td></tr><tr><th>2</th><td>050</td><td>3</td><td>6</td><td>01</td><td>001</td><td>Alabama</td><td>Autauga County</td><td>54571</td></tr><tr><th>3</th><td>050</td><td>3</td><td>6</td><td>01</td><td>003</td><td>Alabama</td><td>Baldwin County</td><td>182265</td></tr><tr><th>4</th><td>050</td><td>3</td><td>6</td><td>01</td><td>005</td><td>Alabama</td><td>Barbour County</td><td>27457</td></tr><tr><th>5</th><td>050</td><td>3</td><td>6</td><td>01</td><td>007</td><td>Alabama</td><td>Bibb County</td><td>22915</td></tr></tbody></table>"
      ],
      "text/latex": [
       "\\begin{tabular}{r|ccccccccc}\n",
       "\t& SUMLEV & REGION & DIVISION & STATE & COUNTY & STNAME & CTYNAME & CENSUS2010POP & \\\\\n",
       "\t\\hline\n",
       "\t& String & String & String & String & String & String & String & String & \\\\\n",
       "\t\\hline\n",
       "\t1 & 040 & 3 & 6 & 01 & 000 & Alabama & Alabama & 4779736 & $\\dots$ \\\\\n",
       "\t2 & 050 & 3 & 6 & 01 & 001 & Alabama & Autauga County & 54571 & $\\dots$ \\\\\n",
       "\t3 & 050 & 3 & 6 & 01 & 003 & Alabama & Baldwin County & 182265 & $\\dots$ \\\\\n",
       "\t4 & 050 & 3 & 6 & 01 & 005 & Alabama & Barbour County & 27457 & $\\dots$ \\\\\n",
       "\t5 & 050 & 3 & 6 & 01 & 007 & Alabama & Bibb County & 22915 & $\\dots$ \\\\\n",
       "\\end{tabular}\n"
      ],
      "text/plain": [
       "5×164 DataFrame. Omitted printing of 158 columns\n",
       "│ Row │ SUMLEV │ REGION │ DIVISION │ STATE  │ COUNTY │ STNAME  │\n",
       "│     │ \u001b[90mString\u001b[39m │ \u001b[90mString\u001b[39m │ \u001b[90mString\u001b[39m   │ \u001b[90mString\u001b[39m │ \u001b[90mString\u001b[39m │ \u001b[90mString\u001b[39m  │\n",
       "├─────┼────────┼────────┼──────────┼────────┼────────┼─────────┤\n",
       "│ 1   │ 040    │ 3      │ 6        │ 01     │ 000    │ Alabama │\n",
       "│ 2   │ 050    │ 3      │ 6        │ 01     │ 001    │ Alabama │\n",
       "│ 3   │ 050    │ 3      │ 6        │ 01     │ 003    │ Alabama │\n",
       "│ 4   │ 050    │ 3      │ 6        │ 01     │ 005    │ Alabama │\n",
       "│ 5   │ 050    │ 3      │ 6        │ 01     │ 007    │ Alabama │"
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df = CSV.read(\"us_census.csv\",silencewarnings=true,type=String)\n",
    "first(df,5)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "164-element Array{String,1}:\n",
       " \"SUMLEV\"\n",
       " \"REGION\"\n",
       " \"DIVISION\"\n",
       " \"STATE\"\n",
       " \"COUNTY\"\n",
       " \"STNAME\"\n",
       " \"CTYNAME\"\n",
       " \"CENSUS2010POP\"\n",
       " \"ESTIMATESBASE2010\"\n",
       " \"POPESTIMATE2010\"\n",
       " \"POPESTIMATE2011\"\n",
       " \"POPESTIMATE2012\"\n",
       " \"POPESTIMATE2013\"\n",
       " ⋮\n",
       " \"RDOMESTICMIG2017\"\n",
       " \"RDOMESTICMIG2018\"\n",
       " \"RDOMESTICMIG2019\"\n",
       " \"RNETMIG2011\"\n",
       " \"RNETMIG2012\"\n",
       " \"RNETMIG2013\"\n",
       " \"RNETMIG2014\"\n",
       " \"RNETMIG2015\"\n",
       " \"RNETMIG2016\"\n",
       " \"RNETMIG2017\"\n",
       " \"RNETMIG2018\"\n",
       " \"RNETMIG2019\""
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "names(df)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table class=\"data-frame\"><thead><tr><th></th><th>STATE</th><th>COUNTY</th><th>STNAME</th><th>CTYNAME</th><th>POPESTIMATE2019</th></tr><tr><th></th><th>String</th><th>String</th><th>String</th><th>String</th><th>String</th></tr></thead><tbody><p>5 rows × 5 columns</p><tr><th>1</th><td>01</td><td>000</td><td>Alabama</td><td>Alabama</td><td>4903185</td></tr><tr><th>2</th><td>01</td><td>001</td><td>Alabama</td><td>Autauga County</td><td>55869</td></tr><tr><th>3</th><td>01</td><td>003</td><td>Alabama</td><td>Baldwin County</td><td>223234</td></tr><tr><th>4</th><td>01</td><td>005</td><td>Alabama</td><td>Barbour County</td><td>24686</td></tr><tr><th>5</th><td>01</td><td>007</td><td>Alabama</td><td>Bibb County</td><td>22394</td></tr></tbody></table>"
      ],
      "text/latex": [
       "\\begin{tabular}{r|ccccc}\n",
       "\t& STATE & COUNTY & STNAME & CTYNAME & POPESTIMATE2019\\\\\n",
       "\t\\hline\n",
       "\t& String & String & String & String & String\\\\\n",
       "\t\\hline\n",
       "\t1 & 01 & 000 & Alabama & Alabama & 4903185 \\\\\n",
       "\t2 & 01 & 001 & Alabama & Autauga County & 55869 \\\\\n",
       "\t3 & 01 & 003 & Alabama & Baldwin County & 223234 \\\\\n",
       "\t4 & 01 & 005 & Alabama & Barbour County & 24686 \\\\\n",
       "\t5 & 01 & 007 & Alabama & Bibb County & 22394 \\\\\n",
       "\\end{tabular}\n"
      ],
      "text/plain": [
       "5×5 DataFrame\n",
       "│ Row │ STATE  │ COUNTY │ STNAME  │ CTYNAME        │ POPESTIMATE2019 │\n",
       "│     │ \u001b[90mString\u001b[39m │ \u001b[90mString\u001b[39m │ \u001b[90mString\u001b[39m  │ \u001b[90mString\u001b[39m         │ \u001b[90mString\u001b[39m          │\n",
       "├─────┼────────┼────────┼─────────┼────────────────┼─────────────────┤\n",
       "│ 1   │ 01     │ 000    │ Alabama │ Alabama        │ 4903185         │\n",
       "│ 2   │ 01     │ 001    │ Alabama │ Autauga County │ 55869           │\n",
       "│ 3   │ 01     │ 003    │ Alabama │ Baldwin County │ 223234          │\n",
       "│ 4   │ 01     │ 005    │ Alabama │ Barbour County │ 24686           │\n",
       "│ 5   │ 01     │ 007    │ Alabama │ Bibb County    │ 22394           │"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dfc = df[:,[:STATE,:COUNTY,:STNAME,:CTYNAME,:POPESTIMATE2019]]\n",
    "first(dfc,5)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### Add a FIPS Column combining STATE and COUNTY Codes"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table class=\"data-frame\"><thead><tr><th></th><th>STATE</th><th>COUNTY</th><th>STNAME</th><th>CTYNAME</th><th>FIPS</th><th>POPESTIMATE2019</th></tr><tr><th></th><th>String</th><th>String</th><th>String</th><th>String</th><th>String</th><th>String</th></tr></thead><tbody><p>5 rows × 6 columns</p><tr><th>1</th><td>01</td><td>000</td><td>Alabama</td><td>Alabama</td><td>01000</td><td>4903185</td></tr><tr><th>2</th><td>01</td><td>001</td><td>Alabama</td><td>Autauga County</td><td>01001</td><td>55869</td></tr><tr><th>3</th><td>01</td><td>003</td><td>Alabama</td><td>Baldwin County</td><td>01003</td><td>223234</td></tr><tr><th>4</th><td>01</td><td>005</td><td>Alabama</td><td>Barbour County</td><td>01005</td><td>24686</td></tr><tr><th>5</th><td>01</td><td>007</td><td>Alabama</td><td>Bibb County</td><td>01007</td><td>22394</td></tr></tbody></table>"
      ],
      "text/latex": [
       "\\begin{tabular}{r|cccccc}\n",
       "\t& STATE & COUNTY & STNAME & CTYNAME & FIPS & POPESTIMATE2019\\\\\n",
       "\t\\hline\n",
       "\t& String & String & String & String & String & String\\\\\n",
       "\t\\hline\n",
       "\t1 & 01 & 000 & Alabama & Alabama & 01000 & 4903185 \\\\\n",
       "\t2 & 01 & 001 & Alabama & Autauga County & 01001 & 55869 \\\\\n",
       "\t3 & 01 & 003 & Alabama & Baldwin County & 01003 & 223234 \\\\\n",
       "\t4 & 01 & 005 & Alabama & Barbour County & 01005 & 24686 \\\\\n",
       "\t5 & 01 & 007 & Alabama & Bibb County & 01007 & 22394 \\\\\n",
       "\\end{tabular}\n"
      ],
      "text/plain": [
       "5×6 DataFrame\n",
       "│ Row │ STATE  │ COUNTY │ STNAME  │ CTYNAME        │ FIPS   │ POPESTIMATE2019 │\n",
       "│     │ \u001b[90mString\u001b[39m │ \u001b[90mString\u001b[39m │ \u001b[90mString\u001b[39m  │ \u001b[90mString\u001b[39m         │ \u001b[90mString\u001b[39m │ \u001b[90mString\u001b[39m          │\n",
       "├─────┼────────┼────────┼─────────┼────────────────┼────────┼─────────────────┤\n",
       "│ 1   │ 01     │ 000    │ Alabama │ Alabama        │ 01000  │ 4903185         │\n",
       "│ 2   │ 01     │ 001    │ Alabama │ Autauga County │ 01001  │ 55869           │\n",
       "│ 3   │ 01     │ 003    │ Alabama │ Baldwin County │ 01003  │ 223234          │\n",
       "│ 4   │ 01     │ 005    │ Alabama │ Barbour County │ 01005  │ 24686           │\n",
       "│ 5   │ 01     │ 007    │ Alabama │ Bibb County    │ 01007  │ 22394           │"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "insertcols!(dfc, 5, \"FIPS\"=>(dfc.STATE .* dfc.COUNTY))\n",
    "first(dfc,5)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### States have a County Code of 000"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table class=\"data-frame\"><thead><tr><th></th><th>FIPS</th><th>STNAME</th><th>POPESTIMATE2019</th></tr><tr><th></th><th>String</th><th>String</th><th>String</th></tr></thead><tbody><p>51 rows × 3 columns</p><tr><th>1</th><td>01000</td><td>Alabama</td><td>4903185</td></tr><tr><th>2</th><td>02000</td><td>Alaska</td><td>731545</td></tr><tr><th>3</th><td>04000</td><td>Arizona</td><td>7278717</td></tr><tr><th>4</th><td>05000</td><td>Arkansas</td><td>3017804</td></tr><tr><th>5</th><td>06000</td><td>California</td><td>39512223</td></tr><tr><th>6</th><td>08000</td><td>Colorado</td><td>5758736</td></tr><tr><th>7</th><td>09000</td><td>Connecticut</td><td>3565287</td></tr><tr><th>8</th><td>10000</td><td>Delaware</td><td>973764</td></tr><tr><th>9</th><td>11000</td><td>District of Columbia</td><td>705749</td></tr><tr><th>10</th><td>12000</td><td>Florida</td><td>21477737</td></tr><tr><th>11</th><td>13000</td><td>Georgia</td><td>10617423</td></tr><tr><th>12</th><td>15000</td><td>Hawaii</td><td>1415872</td></tr><tr><th>13</th><td>16000</td><td>Idaho</td><td>1787065</td></tr><tr><th>14</th><td>17000</td><td>Illinois</td><td>12671821</td></tr><tr><th>15</th><td>18000</td><td>Indiana</td><td>6732219</td></tr><tr><th>16</th><td>19000</td><td>Iowa</td><td>3155070</td></tr><tr><th>17</th><td>20000</td><td>Kansas</td><td>2913314</td></tr><tr><th>18</th><td>21000</td><td>Kentucky</td><td>4467673</td></tr><tr><th>19</th><td>22000</td><td>Louisiana</td><td>4648794</td></tr><tr><th>20</th><td>23000</td><td>Maine</td><td>1344212</td></tr><tr><th>21</th><td>24000</td><td>Maryland</td><td>6045680</td></tr><tr><th>22</th><td>25000</td><td>Massachusetts</td><td>6892503</td></tr><tr><th>23</th><td>26000</td><td>Michigan</td><td>9986857</td></tr><tr><th>24</th><td>27000</td><td>Minnesota</td><td>5639632</td></tr><tr><th>25</th><td>28000</td><td>Mississippi</td><td>2976149</td></tr><tr><th>26</th><td>29000</td><td>Missouri</td><td>6137428</td></tr><tr><th>27</th><td>30000</td><td>Montana</td><td>1068778</td></tr><tr><th>28</th><td>31000</td><td>Nebraska</td><td>1934408</td></tr><tr><th>29</th><td>32000</td><td>Nevada</td><td>3080156</td></tr><tr><th>30</th><td>33000</td><td>New Hampshire</td><td>1359711</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>"
      ],
      "text/latex": [
       "\\begin{tabular}{r|ccc}\n",
       "\t& FIPS & STNAME & POPESTIMATE2019\\\\\n",
       "\t\\hline\n",
       "\t& String & String & String\\\\\n",
       "\t\\hline\n",
       "\t1 & 01000 & Alabama & 4903185 \\\\\n",
       "\t2 & 02000 & Alaska & 731545 \\\\\n",
       "\t3 & 04000 & Arizona & 7278717 \\\\\n",
       "\t4 & 05000 & Arkansas & 3017804 \\\\\n",
       "\t5 & 06000 & California & 39512223 \\\\\n",
       "\t6 & 08000 & Colorado & 5758736 \\\\\n",
       "\t7 & 09000 & Connecticut & 3565287 \\\\\n",
       "\t8 & 10000 & Delaware & 973764 \\\\\n",
       "\t9 & 11000 & District of Columbia & 705749 \\\\\n",
       "\t10 & 12000 & Florida & 21477737 \\\\\n",
       "\t11 & 13000 & Georgia & 10617423 \\\\\n",
       "\t12 & 15000 & Hawaii & 1415872 \\\\\n",
       "\t13 & 16000 & Idaho & 1787065 \\\\\n",
       "\t14 & 17000 & Illinois & 12671821 \\\\\n",
       "\t15 & 18000 & Indiana & 6732219 \\\\\n",
       "\t16 & 19000 & Iowa & 3155070 \\\\\n",
       "\t17 & 20000 & Kansas & 2913314 \\\\\n",
       "\t18 & 21000 & Kentucky & 4467673 \\\\\n",
       "\t19 & 22000 & Louisiana & 4648794 \\\\\n",
       "\t20 & 23000 & Maine & 1344212 \\\\\n",
       "\t21 & 24000 & Maryland & 6045680 \\\\\n",
       "\t22 & 25000 & Massachusetts & 6892503 \\\\\n",
       "\t23 & 26000 & Michigan & 9986857 \\\\\n",
       "\t24 & 27000 & Minnesota & 5639632 \\\\\n",
       "\t25 & 28000 & Mississippi & 2976149 \\\\\n",
       "\t26 & 29000 & Missouri & 6137428 \\\\\n",
       "\t27 & 30000 & Montana & 1068778 \\\\\n",
       "\t28 & 31000 & Nebraska & 1934408 \\\\\n",
       "\t29 & 32000 & Nevada & 3080156 \\\\\n",
       "\t30 & 33000 & New Hampshire & 1359711 \\\\\n",
       "\t$\\dots$ & $\\dots$ & $\\dots$ & $\\dots$ \\\\\n",
       "\\end{tabular}\n"
      ],
      "text/plain": [
       "51×3 DataFrame\n",
       "│ Row │ FIPS   │ STNAME               │ POPESTIMATE2019 │\n",
       "│     │ \u001b[90mString\u001b[39m │ \u001b[90mString\u001b[39m               │ \u001b[90mString\u001b[39m          │\n",
       "├─────┼────────┼──────────────────────┼─────────────────┤\n",
       "│ 1   │ 01000  │ Alabama              │ 4903185         │\n",
       "│ 2   │ 02000  │ Alaska               │ 731545          │\n",
       "│ 3   │ 04000  │ Arizona              │ 7278717         │\n",
       "│ 4   │ 05000  │ Arkansas             │ 3017804         │\n",
       "│ 5   │ 06000  │ California           │ 39512223        │\n",
       "│ 6   │ 08000  │ Colorado             │ 5758736         │\n",
       "│ 7   │ 09000  │ Connecticut          │ 3565287         │\n",
       "│ 8   │ 10000  │ Delaware             │ 973764          │\n",
       "│ 9   │ 11000  │ District of Columbia │ 705749          │\n",
       "│ 10  │ 12000  │ Florida              │ 21477737        │\n",
       "⋮\n",
       "│ 41  │ 45000  │ South Carolina       │ 5148714         │\n",
       "│ 42  │ 46000  │ South Dakota         │ 884659          │\n",
       "│ 43  │ 47000  │ Tennessee            │ 6829174         │\n",
       "│ 44  │ 48000  │ Texas                │ 28995881        │\n",
       "│ 45  │ 49000  │ Utah                 │ 3205958         │\n",
       "│ 46  │ 50000  │ Vermont              │ 623989          │\n",
       "│ 47  │ 51000  │ Virginia             │ 8535519         │\n",
       "│ 48  │ 53000  │ Washington           │ 7614893         │\n",
       "│ 49  │ 54000  │ West Virginia        │ 1792147         │\n",
       "│ 50  │ 55000  │ Wisconsin            │ 5822434         │\n",
       "│ 51  │ 56000  │ Wyoming              │ 578759          │"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "filter(r->r.COUNTY == \"000\",dfc)[:,[:FIPS,:STNAME,:POPESTIMATE2019]]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "\"2019_state_populations.csv\""
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "CSV.write(\"2019_state_populations.csv\", \n",
    "    filter(r->r.COUNTY == \"000\",dfc)[:,[:FIPS,:STNAME,:POPESTIMATE2019]],\n",
    "    header = [:fips,:state,:population])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table class=\"data-frame\"><thead><tr><th></th><th>fips</th><th>state</th><th>population</th></tr><tr><th></th><th>String</th><th>String</th><th>String</th></tr></thead><tbody><p>51 rows × 3 columns</p><tr><th>1</th><td>01000</td><td>Alabama</td><td>4903185</td></tr><tr><th>2</th><td>02000</td><td>Alaska</td><td>731545</td></tr><tr><th>3</th><td>04000</td><td>Arizona</td><td>7278717</td></tr><tr><th>4</th><td>05000</td><td>Arkansas</td><td>3017804</td></tr><tr><th>5</th><td>06000</td><td>California</td><td>39512223</td></tr><tr><th>6</th><td>08000</td><td>Colorado</td><td>5758736</td></tr><tr><th>7</th><td>09000</td><td>Connecticut</td><td>3565287</td></tr><tr><th>8</th><td>10000</td><td>Delaware</td><td>973764</td></tr><tr><th>9</th><td>11000</td><td>District of Columbia</td><td>705749</td></tr><tr><th>10</th><td>12000</td><td>Florida</td><td>21477737</td></tr><tr><th>11</th><td>13000</td><td>Georgia</td><td>10617423</td></tr><tr><th>12</th><td>15000</td><td>Hawaii</td><td>1415872</td></tr><tr><th>13</th><td>16000</td><td>Idaho</td><td>1787065</td></tr><tr><th>14</th><td>17000</td><td>Illinois</td><td>12671821</td></tr><tr><th>15</th><td>18000</td><td>Indiana</td><td>6732219</td></tr><tr><th>16</th><td>19000</td><td>Iowa</td><td>3155070</td></tr><tr><th>17</th><td>20000</td><td>Kansas</td><td>2913314</td></tr><tr><th>18</th><td>21000</td><td>Kentucky</td><td>4467673</td></tr><tr><th>19</th><td>22000</td><td>Louisiana</td><td>4648794</td></tr><tr><th>20</th><td>23000</td><td>Maine</td><td>1344212</td></tr><tr><th>21</th><td>24000</td><td>Maryland</td><td>6045680</td></tr><tr><th>22</th><td>25000</td><td>Massachusetts</td><td>6892503</td></tr><tr><th>23</th><td>26000</td><td>Michigan</td><td>9986857</td></tr><tr><th>24</th><td>27000</td><td>Minnesota</td><td>5639632</td></tr><tr><th>25</th><td>28000</td><td>Mississippi</td><td>2976149</td></tr><tr><th>26</th><td>29000</td><td>Missouri</td><td>6137428</td></tr><tr><th>27</th><td>30000</td><td>Montana</td><td>1068778</td></tr><tr><th>28</th><td>31000</td><td>Nebraska</td><td>1934408</td></tr><tr><th>29</th><td>32000</td><td>Nevada</td><td>3080156</td></tr><tr><th>30</th><td>33000</td><td>New Hampshire</td><td>1359711</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>"
      ],
      "text/latex": [
       "\\begin{tabular}{r|ccc}\n",
       "\t& fips & state & population\\\\\n",
       "\t\\hline\n",
       "\t& String & String & String\\\\\n",
       "\t\\hline\n",
       "\t1 & 01000 & Alabama & 4903185 \\\\\n",
       "\t2 & 02000 & Alaska & 731545 \\\\\n",
       "\t3 & 04000 & Arizona & 7278717 \\\\\n",
       "\t4 & 05000 & Arkansas & 3017804 \\\\\n",
       "\t5 & 06000 & California & 39512223 \\\\\n",
       "\t6 & 08000 & Colorado & 5758736 \\\\\n",
       "\t7 & 09000 & Connecticut & 3565287 \\\\\n",
       "\t8 & 10000 & Delaware & 973764 \\\\\n",
       "\t9 & 11000 & District of Columbia & 705749 \\\\\n",
       "\t10 & 12000 & Florida & 21477737 \\\\\n",
       "\t11 & 13000 & Georgia & 10617423 \\\\\n",
       "\t12 & 15000 & Hawaii & 1415872 \\\\\n",
       "\t13 & 16000 & Idaho & 1787065 \\\\\n",
       "\t14 & 17000 & Illinois & 12671821 \\\\\n",
       "\t15 & 18000 & Indiana & 6732219 \\\\\n",
       "\t16 & 19000 & Iowa & 3155070 \\\\\n",
       "\t17 & 20000 & Kansas & 2913314 \\\\\n",
       "\t18 & 21000 & Kentucky & 4467673 \\\\\n",
       "\t19 & 22000 & Louisiana & 4648794 \\\\\n",
       "\t20 & 23000 & Maine & 1344212 \\\\\n",
       "\t21 & 24000 & Maryland & 6045680 \\\\\n",
       "\t22 & 25000 & Massachusetts & 6892503 \\\\\n",
       "\t23 & 26000 & Michigan & 9986857 \\\\\n",
       "\t24 & 27000 & Minnesota & 5639632 \\\\\n",
       "\t25 & 28000 & Mississippi & 2976149 \\\\\n",
       "\t26 & 29000 & Missouri & 6137428 \\\\\n",
       "\t27 & 30000 & Montana & 1068778 \\\\\n",
       "\t28 & 31000 & Nebraska & 1934408 \\\\\n",
       "\t29 & 32000 & Nevada & 3080156 \\\\\n",
       "\t30 & 33000 & New Hampshire & 1359711 \\\\\n",
       "\t$\\dots$ & $\\dots$ & $\\dots$ & $\\dots$ \\\\\n",
       "\\end{tabular}\n"
      ],
      "text/plain": [
       "51×3 DataFrame\n",
       "│ Row │ fips   │ state                │ population │\n",
       "│     │ \u001b[90mString\u001b[39m │ \u001b[90mString\u001b[39m               │ \u001b[90mString\u001b[39m     │\n",
       "├─────┼────────┼──────────────────────┼────────────┤\n",
       "│ 1   │ 01000  │ Alabama              │ 4903185    │\n",
       "│ 2   │ 02000  │ Alaska               │ 731545     │\n",
       "│ 3   │ 04000  │ Arizona              │ 7278717    │\n",
       "│ 4   │ 05000  │ Arkansas             │ 3017804    │\n",
       "│ 5   │ 06000  │ California           │ 39512223   │\n",
       "│ 6   │ 08000  │ Colorado             │ 5758736    │\n",
       "│ 7   │ 09000  │ Connecticut          │ 3565287    │\n",
       "│ 8   │ 10000  │ Delaware             │ 973764     │\n",
       "│ 9   │ 11000  │ District of Columbia │ 705749     │\n",
       "│ 10  │ 12000  │ Florida              │ 21477737   │\n",
       "⋮\n",
       "│ 41  │ 45000  │ South Carolina       │ 5148714    │\n",
       "│ 42  │ 46000  │ South Dakota         │ 884659     │\n",
       "│ 43  │ 47000  │ Tennessee            │ 6829174    │\n",
       "│ 44  │ 48000  │ Texas                │ 28995881   │\n",
       "│ 45  │ 49000  │ Utah                 │ 3205958    │\n",
       "│ 46  │ 50000  │ Vermont              │ 623989     │\n",
       "│ 47  │ 51000  │ Virginia             │ 8535519    │\n",
       "│ 48  │ 53000  │ Washington           │ 7614893    │\n",
       "│ 49  │ 54000  │ West Virginia        │ 1792147    │\n",
       "│ 50  │ 55000  │ Wisconsin            │ 5822434    │\n",
       "│ 51  │ 56000  │ Wyoming              │ 578759     │"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "state_pops = CSV.read(\"2019_state_populations.csv\",type=String)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### States have a County Code other than 000"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "\"2019_county_populations.csv\""
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "CSV.write(\"2019_county_populations.csv\", \n",
    "    filter(r->r.COUNTY != \"000\",dfc)[:,[:FIPS,:STNAME,:CTYNAME,:POPESTIMATE2019]],\n",
    "    header = [:fips,:state,:county,:population])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table class=\"data-frame\"><thead><tr><th></th><th>fips</th><th>state</th><th>county</th><th>population</th></tr><tr><th></th><th>String</th><th>String</th><th>String</th><th>Int64</th></tr></thead><tbody><p>3,142 rows × 4 columns</p><tr><th>1</th><td>01001</td><td>Alabama</td><td>Autauga County</td><td>55869</td></tr><tr><th>2</th><td>01003</td><td>Alabama</td><td>Baldwin County</td><td>223234</td></tr><tr><th>3</th><td>01005</td><td>Alabama</td><td>Barbour County</td><td>24686</td></tr><tr><th>4</th><td>01007</td><td>Alabama</td><td>Bibb County</td><td>22394</td></tr><tr><th>5</th><td>01009</td><td>Alabama</td><td>Blount County</td><td>57826</td></tr><tr><th>6</th><td>01011</td><td>Alabama</td><td>Bullock County</td><td>10101</td></tr><tr><th>7</th><td>01013</td><td>Alabama</td><td>Butler County</td><td>19448</td></tr><tr><th>8</th><td>01015</td><td>Alabama</td><td>Calhoun County</td><td>113605</td></tr><tr><th>9</th><td>01017</td><td>Alabama</td><td>Chambers County</td><td>33254</td></tr><tr><th>10</th><td>01019</td><td>Alabama</td><td>Cherokee County</td><td>26196</td></tr><tr><th>11</th><td>01021</td><td>Alabama</td><td>Chilton County</td><td>44428</td></tr><tr><th>12</th><td>01023</td><td>Alabama</td><td>Choctaw County</td><td>12589</td></tr><tr><th>13</th><td>01025</td><td>Alabama</td><td>Clarke County</td><td>23622</td></tr><tr><th>14</th><td>01027</td><td>Alabama</td><td>Clay County</td><td>13235</td></tr><tr><th>15</th><td>01029</td><td>Alabama</td><td>Cleburne County</td><td>14910</td></tr><tr><th>16</th><td>01031</td><td>Alabama</td><td>Coffee County</td><td>52342</td></tr><tr><th>17</th><td>01033</td><td>Alabama</td><td>Colbert County</td><td>55241</td></tr><tr><th>18</th><td>01035</td><td>Alabama</td><td>Conecuh County</td><td>12067</td></tr><tr><th>19</th><td>01037</td><td>Alabama</td><td>Coosa County</td><td>10663</td></tr><tr><th>20</th><td>01039</td><td>Alabama</td><td>Covington County</td><td>37049</td></tr><tr><th>21</th><td>01041</td><td>Alabama</td><td>Crenshaw County</td><td>13772</td></tr><tr><th>22</th><td>01043</td><td>Alabama</td><td>Cullman County</td><td>83768</td></tr><tr><th>23</th><td>01045</td><td>Alabama</td><td>Dale County</td><td>49172</td></tr><tr><th>24</th><td>01047</td><td>Alabama</td><td>Dallas County</td><td>37196</td></tr><tr><th>25</th><td>01049</td><td>Alabama</td><td>DeKalb County</td><td>71513</td></tr><tr><th>26</th><td>01051</td><td>Alabama</td><td>Elmore County</td><td>81209</td></tr><tr><th>27</th><td>01053</td><td>Alabama</td><td>Escambia County</td><td>36633</td></tr><tr><th>28</th><td>01055</td><td>Alabama</td><td>Etowah County</td><td>102268</td></tr><tr><th>29</th><td>01057</td><td>Alabama</td><td>Fayette County</td><td>16302</td></tr><tr><th>30</th><td>01059</td><td>Alabama</td><td>Franklin County</td><td>31362</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>"
      ],
      "text/latex": [
       "\\begin{tabular}{r|cccc}\n",
       "\t& fips & state & county & population\\\\\n",
       "\t\\hline\n",
       "\t& String & String & String & Int64\\\\\n",
       "\t\\hline\n",
       "\t1 & 01001 & Alabama & Autauga County & 55869 \\\\\n",
       "\t2 & 01003 & Alabama & Baldwin County & 223234 \\\\\n",
       "\t3 & 01005 & Alabama & Barbour County & 24686 \\\\\n",
       "\t4 & 01007 & Alabama & Bibb County & 22394 \\\\\n",
       "\t5 & 01009 & Alabama & Blount County & 57826 \\\\\n",
       "\t6 & 01011 & Alabama & Bullock County & 10101 \\\\\n",
       "\t7 & 01013 & Alabama & Butler County & 19448 \\\\\n",
       "\t8 & 01015 & Alabama & Calhoun County & 113605 \\\\\n",
       "\t9 & 01017 & Alabama & Chambers County & 33254 \\\\\n",
       "\t10 & 01019 & Alabama & Cherokee County & 26196 \\\\\n",
       "\t11 & 01021 & Alabama & Chilton County & 44428 \\\\\n",
       "\t12 & 01023 & Alabama & Choctaw County & 12589 \\\\\n",
       "\t13 & 01025 & Alabama & Clarke County & 23622 \\\\\n",
       "\t14 & 01027 & Alabama & Clay County & 13235 \\\\\n",
       "\t15 & 01029 & Alabama & Cleburne County & 14910 \\\\\n",
       "\t16 & 01031 & Alabama & Coffee County & 52342 \\\\\n",
       "\t17 & 01033 & Alabama & Colbert County & 55241 \\\\\n",
       "\t18 & 01035 & Alabama & Conecuh County & 12067 \\\\\n",
       "\t19 & 01037 & Alabama & Coosa County & 10663 \\\\\n",
       "\t20 & 01039 & Alabama & Covington County & 37049 \\\\\n",
       "\t21 & 01041 & Alabama & Crenshaw County & 13772 \\\\\n",
       "\t22 & 01043 & Alabama & Cullman County & 83768 \\\\\n",
       "\t23 & 01045 & Alabama & Dale County & 49172 \\\\\n",
       "\t24 & 01047 & Alabama & Dallas County & 37196 \\\\\n",
       "\t25 & 01049 & Alabama & DeKalb County & 71513 \\\\\n",
       "\t26 & 01051 & Alabama & Elmore County & 81209 \\\\\n",
       "\t27 & 01053 & Alabama & Escambia County & 36633 \\\\\n",
       "\t28 & 01055 & Alabama & Etowah County & 102268 \\\\\n",
       "\t29 & 01057 & Alabama & Fayette County & 16302 \\\\\n",
       "\t30 & 01059 & Alabama & Franklin County & 31362 \\\\\n",
       "\t$\\dots$ & $\\dots$ & $\\dots$ & $\\dots$ & $\\dots$ \\\\\n",
       "\\end{tabular}\n"
      ],
      "text/plain": [
       "3142×4 DataFrame\n",
       "│ Row  │ fips   │ state   │ county            │ population │\n",
       "│      │ \u001b[90mString\u001b[39m │ \u001b[90mString\u001b[39m  │ \u001b[90mString\u001b[39m            │ \u001b[90mInt64\u001b[39m      │\n",
       "├──────┼────────┼─────────┼───────────────────┼────────────┤\n",
       "│ 1    │ 01001  │ Alabama │ Autauga County    │ 55869      │\n",
       "│ 2    │ 01003  │ Alabama │ Baldwin County    │ 223234     │\n",
       "│ 3    │ 01005  │ Alabama │ Barbour County    │ 24686      │\n",
       "│ 4    │ 01007  │ Alabama │ Bibb County       │ 22394      │\n",
       "│ 5    │ 01009  │ Alabama │ Blount County     │ 57826      │\n",
       "│ 6    │ 01011  │ Alabama │ Bullock County    │ 10101      │\n",
       "│ 7    │ 01013  │ Alabama │ Butler County     │ 19448      │\n",
       "│ 8    │ 01015  │ Alabama │ Calhoun County    │ 113605     │\n",
       "│ 9    │ 01017  │ Alabama │ Chambers County   │ 33254      │\n",
       "│ 10   │ 01019  │ Alabama │ Cherokee County   │ 26196      │\n",
       "⋮\n",
       "│ 3132 │ 56025  │ Wyoming │ Natrona County    │ 79858      │\n",
       "│ 3133 │ 56027  │ Wyoming │ Niobrara County   │ 2356       │\n",
       "│ 3134 │ 56029  │ Wyoming │ Park County       │ 29194      │\n",
       "│ 3135 │ 56031  │ Wyoming │ Platte County     │ 8393       │\n",
       "│ 3136 │ 56033  │ Wyoming │ Sheridan County   │ 30485      │\n",
       "│ 3137 │ 56035  │ Wyoming │ Sublette County   │ 9831       │\n",
       "│ 3138 │ 56037  │ Wyoming │ Sweetwater County │ 42343      │\n",
       "│ 3139 │ 56039  │ Wyoming │ Teton County      │ 23464      │\n",
       "│ 3140 │ 56041  │ Wyoming │ Uinta County      │ 20226      │\n",
       "│ 3141 │ 56043  │ Wyoming │ Washakie County   │ 7805       │\n",
       "│ 3142 │ 56045  │ Wyoming │ Weston County     │ 6927       │"
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "county_pops = CSV.read(\"2019_county_populations.csv\",type=String,types=Dict(4=>Int64))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "#### Look up Cook County"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table class=\"data-frame\"><thead><tr><th></th><th>fips</th><th>state</th><th>county</th><th>population</th></tr><tr><th></th><th>String</th><th>String</th><th>String</th><th>Int64</th></tr></thead><tbody><p>1 rows × 4 columns</p><tr><th>1</th><td>17031</td><td>Illinois</td><td>Cook County</td><td>5150233</td></tr></tbody></table>"
      ],
      "text/latex": [
       "\\begin{tabular}{r|cccc}\n",
       "\t& fips & state & county & population\\\\\n",
       "\t\\hline\n",
       "\t& String & String & String & Int64\\\\\n",
       "\t\\hline\n",
       "\t1 & 17031 & Illinois & Cook County & 5150233 \\\\\n",
       "\\end{tabular}\n"
      ],
      "text/plain": [
       "1×4 DataFrame\n",
       "│ Row │ fips   │ state    │ county      │ population │\n",
       "│     │ \u001b[90mString\u001b[39m │ \u001b[90mString\u001b[39m   │ \u001b[90mString\u001b[39m      │ \u001b[90mInt64\u001b[39m      │\n",
       "├─────┼────────┼──────────┼─────────────┼────────────┤\n",
       "│ 1   │ 17031  │ Illinois │ Cook County │ 5150233    │"
      ]
     },
     "execution_count": 13,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "filter(r-> r.state==\"Illinois\" && r.county==\"Cook County\",county_pops)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table class=\"data-frame\"><thead><tr><th></th><th>fips</th><th>state</th><th>county</th><th>population</th></tr><tr><th></th><th>String</th><th>String</th><th>String</th><th>Int64</th></tr></thead><tbody><p>1 rows × 4 columns</p><tr><th>1</th><td>17031</td><td>Illinois</td><td>Cook County</td><td>5150233</td></tr></tbody></table>"
      ],
      "text/latex": [
       "\\begin{tabular}{r|cccc}\n",
       "\t& fips & state & county & population\\\\\n",
       "\t\\hline\n",
       "\t& String & String & String & Int64\\\\\n",
       "\t\\hline\n",
       "\t1 & 17031 & Illinois & Cook County & 5150233 \\\\\n",
       "\\end{tabular}\n"
      ],
      "text/plain": [
       "1×4 DataFrame\n",
       "│ Row │ fips   │ state    │ county      │ population │\n",
       "│     │ \u001b[90mString\u001b[39m │ \u001b[90mString\u001b[39m   │ \u001b[90mString\u001b[39m      │ \u001b[90mInt64\u001b[39m      │\n",
       "├─────┼────────┼──────────┼─────────────┼────────────┤\n",
       "│ 1   │ 17031  │ Illinois │ Cook County │ 5150233    │"
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "filter(r-> r.fips==\"17031\",county_pops)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Accesor API to get Populations"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### State Populations"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "get_state_populations (generic function with 1 method)"
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "function get_state_populations()\n",
    "    CSV.read(\"2019_state_populations.csv\",type=String,types=Dict(3=>Int64))\n",
    "end"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table class=\"data-frame\"><thead><tr><th></th><th>fips</th><th>state</th><th>population</th></tr><tr><th></th><th>String</th><th>String</th><th>Int64</th></tr></thead><tbody><p>51 rows × 3 columns</p><tr><th>1</th><td>01000</td><td>Alabama</td><td>4903185</td></tr><tr><th>2</th><td>02000</td><td>Alaska</td><td>731545</td></tr><tr><th>3</th><td>04000</td><td>Arizona</td><td>7278717</td></tr><tr><th>4</th><td>05000</td><td>Arkansas</td><td>3017804</td></tr><tr><th>5</th><td>06000</td><td>California</td><td>39512223</td></tr><tr><th>6</th><td>08000</td><td>Colorado</td><td>5758736</td></tr><tr><th>7</th><td>09000</td><td>Connecticut</td><td>3565287</td></tr><tr><th>8</th><td>10000</td><td>Delaware</td><td>973764</td></tr><tr><th>9</th><td>11000</td><td>District of Columbia</td><td>705749</td></tr><tr><th>10</th><td>12000</td><td>Florida</td><td>21477737</td></tr><tr><th>11</th><td>13000</td><td>Georgia</td><td>10617423</td></tr><tr><th>12</th><td>15000</td><td>Hawaii</td><td>1415872</td></tr><tr><th>13</th><td>16000</td><td>Idaho</td><td>1787065</td></tr><tr><th>14</th><td>17000</td><td>Illinois</td><td>12671821</td></tr><tr><th>15</th><td>18000</td><td>Indiana</td><td>6732219</td></tr><tr><th>16</th><td>19000</td><td>Iowa</td><td>3155070</td></tr><tr><th>17</th><td>20000</td><td>Kansas</td><td>2913314</td></tr><tr><th>18</th><td>21000</td><td>Kentucky</td><td>4467673</td></tr><tr><th>19</th><td>22000</td><td>Louisiana</td><td>4648794</td></tr><tr><th>20</th><td>23000</td><td>Maine</td><td>1344212</td></tr><tr><th>21</th><td>24000</td><td>Maryland</td><td>6045680</td></tr><tr><th>22</th><td>25000</td><td>Massachusetts</td><td>6892503</td></tr><tr><th>23</th><td>26000</td><td>Michigan</td><td>9986857</td></tr><tr><th>24</th><td>27000</td><td>Minnesota</td><td>5639632</td></tr><tr><th>25</th><td>28000</td><td>Mississippi</td><td>2976149</td></tr><tr><th>26</th><td>29000</td><td>Missouri</td><td>6137428</td></tr><tr><th>27</th><td>30000</td><td>Montana</td><td>1068778</td></tr><tr><th>28</th><td>31000</td><td>Nebraska</td><td>1934408</td></tr><tr><th>29</th><td>32000</td><td>Nevada</td><td>3080156</td></tr><tr><th>30</th><td>33000</td><td>New Hampshire</td><td>1359711</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>"
      ],
      "text/latex": [
       "\\begin{tabular}{r|ccc}\n",
       "\t& fips & state & population\\\\\n",
       "\t\\hline\n",
       "\t& String & String & Int64\\\\\n",
       "\t\\hline\n",
       "\t1 & 01000 & Alabama & 4903185 \\\\\n",
       "\t2 & 02000 & Alaska & 731545 \\\\\n",
       "\t3 & 04000 & Arizona & 7278717 \\\\\n",
       "\t4 & 05000 & Arkansas & 3017804 \\\\\n",
       "\t5 & 06000 & California & 39512223 \\\\\n",
       "\t6 & 08000 & Colorado & 5758736 \\\\\n",
       "\t7 & 09000 & Connecticut & 3565287 \\\\\n",
       "\t8 & 10000 & Delaware & 973764 \\\\\n",
       "\t9 & 11000 & District of Columbia & 705749 \\\\\n",
       "\t10 & 12000 & Florida & 21477737 \\\\\n",
       "\t11 & 13000 & Georgia & 10617423 \\\\\n",
       "\t12 & 15000 & Hawaii & 1415872 \\\\\n",
       "\t13 & 16000 & Idaho & 1787065 \\\\\n",
       "\t14 & 17000 & Illinois & 12671821 \\\\\n",
       "\t15 & 18000 & Indiana & 6732219 \\\\\n",
       "\t16 & 19000 & Iowa & 3155070 \\\\\n",
       "\t17 & 20000 & Kansas & 2913314 \\\\\n",
       "\t18 & 21000 & Kentucky & 4467673 \\\\\n",
       "\t19 & 22000 & Louisiana & 4648794 \\\\\n",
       "\t20 & 23000 & Maine & 1344212 \\\\\n",
       "\t21 & 24000 & Maryland & 6045680 \\\\\n",
       "\t22 & 25000 & Massachusetts & 6892503 \\\\\n",
       "\t23 & 26000 & Michigan & 9986857 \\\\\n",
       "\t24 & 27000 & Minnesota & 5639632 \\\\\n",
       "\t25 & 28000 & Mississippi & 2976149 \\\\\n",
       "\t26 & 29000 & Missouri & 6137428 \\\\\n",
       "\t27 & 30000 & Montana & 1068778 \\\\\n",
       "\t28 & 31000 & Nebraska & 1934408 \\\\\n",
       "\t29 & 32000 & Nevada & 3080156 \\\\\n",
       "\t30 & 33000 & New Hampshire & 1359711 \\\\\n",
       "\t$\\dots$ & $\\dots$ & $\\dots$ & $\\dots$ \\\\\n",
       "\\end{tabular}\n"
      ],
      "text/plain": [
       "51×3 DataFrame\n",
       "│ Row │ fips   │ state                │ population │\n",
       "│     │ \u001b[90mString\u001b[39m │ \u001b[90mString\u001b[39m               │ \u001b[90mInt64\u001b[39m      │\n",
       "├─────┼────────┼──────────────────────┼────────────┤\n",
       "│ 1   │ 01000  │ Alabama              │ 4903185    │\n",
       "│ 2   │ 02000  │ Alaska               │ 731545     │\n",
       "│ 3   │ 04000  │ Arizona              │ 7278717    │\n",
       "│ 4   │ 05000  │ Arkansas             │ 3017804    │\n",
       "│ 5   │ 06000  │ California           │ 39512223   │\n",
       "│ 6   │ 08000  │ Colorado             │ 5758736    │\n",
       "│ 7   │ 09000  │ Connecticut          │ 3565287    │\n",
       "│ 8   │ 10000  │ Delaware             │ 973764     │\n",
       "│ 9   │ 11000  │ District of Columbia │ 705749     │\n",
       "│ 10  │ 12000  │ Florida              │ 21477737   │\n",
       "⋮\n",
       "│ 41  │ 45000  │ South Carolina       │ 5148714    │\n",
       "│ 42  │ 46000  │ South Dakota         │ 884659     │\n",
       "│ 43  │ 47000  │ Tennessee            │ 6829174    │\n",
       "│ 44  │ 48000  │ Texas                │ 28995881   │\n",
       "│ 45  │ 49000  │ Utah                 │ 3205958    │\n",
       "│ 46  │ 50000  │ Vermont              │ 623989     │\n",
       "│ 47  │ 51000  │ Virginia             │ 8535519    │\n",
       "│ 48  │ 53000  │ Washington           │ 7614893    │\n",
       "│ 49  │ 54000  │ West Virginia        │ 1792147    │\n",
       "│ 50  │ 55000  │ Wisconsin            │ 5822434    │\n",
       "│ 51  │ 56000  │ Wyoming              │ 578759     │"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "get_state_populations()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### County Populations"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "get_county_populations (generic function with 1 method)"
      ]
     },
     "execution_count": 17,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "function get_county_populations()\n",
    "    CSV.read(\"2019_county_populations.csv\",type=String,types=Dict(4=>Int64))\n",
    "end"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<table class=\"data-frame\"><thead><tr><th></th><th>fips</th><th>state</th><th>county</th><th>population</th></tr><tr><th></th><th>String</th><th>String</th><th>String</th><th>Int64</th></tr></thead><tbody><p>3,142 rows × 4 columns</p><tr><th>1</th><td>01001</td><td>Alabama</td><td>Autauga County</td><td>55869</td></tr><tr><th>2</th><td>01003</td><td>Alabama</td><td>Baldwin County</td><td>223234</td></tr><tr><th>3</th><td>01005</td><td>Alabama</td><td>Barbour County</td><td>24686</td></tr><tr><th>4</th><td>01007</td><td>Alabama</td><td>Bibb County</td><td>22394</td></tr><tr><th>5</th><td>01009</td><td>Alabama</td><td>Blount County</td><td>57826</td></tr><tr><th>6</th><td>01011</td><td>Alabama</td><td>Bullock County</td><td>10101</td></tr><tr><th>7</th><td>01013</td><td>Alabama</td><td>Butler County</td><td>19448</td></tr><tr><th>8</th><td>01015</td><td>Alabama</td><td>Calhoun County</td><td>113605</td></tr><tr><th>9</th><td>01017</td><td>Alabama</td><td>Chambers County</td><td>33254</td></tr><tr><th>10</th><td>01019</td><td>Alabama</td><td>Cherokee County</td><td>26196</td></tr><tr><th>11</th><td>01021</td><td>Alabama</td><td>Chilton County</td><td>44428</td></tr><tr><th>12</th><td>01023</td><td>Alabama</td><td>Choctaw County</td><td>12589</td></tr><tr><th>13</th><td>01025</td><td>Alabama</td><td>Clarke County</td><td>23622</td></tr><tr><th>14</th><td>01027</td><td>Alabama</td><td>Clay County</td><td>13235</td></tr><tr><th>15</th><td>01029</td><td>Alabama</td><td>Cleburne County</td><td>14910</td></tr><tr><th>16</th><td>01031</td><td>Alabama</td><td>Coffee County</td><td>52342</td></tr><tr><th>17</th><td>01033</td><td>Alabama</td><td>Colbert County</td><td>55241</td></tr><tr><th>18</th><td>01035</td><td>Alabama</td><td>Conecuh County</td><td>12067</td></tr><tr><th>19</th><td>01037</td><td>Alabama</td><td>Coosa County</td><td>10663</td></tr><tr><th>20</th><td>01039</td><td>Alabama</td><td>Covington County</td><td>37049</td></tr><tr><th>21</th><td>01041</td><td>Alabama</td><td>Crenshaw County</td><td>13772</td></tr><tr><th>22</th><td>01043</td><td>Alabama</td><td>Cullman County</td><td>83768</td></tr><tr><th>23</th><td>01045</td><td>Alabama</td><td>Dale County</td><td>49172</td></tr><tr><th>24</th><td>01047</td><td>Alabama</td><td>Dallas County</td><td>37196</td></tr><tr><th>25</th><td>01049</td><td>Alabama</td><td>DeKalb County</td><td>71513</td></tr><tr><th>26</th><td>01051</td><td>Alabama</td><td>Elmore County</td><td>81209</td></tr><tr><th>27</th><td>01053</td><td>Alabama</td><td>Escambia County</td><td>36633</td></tr><tr><th>28</th><td>01055</td><td>Alabama</td><td>Etowah County</td><td>102268</td></tr><tr><th>29</th><td>01057</td><td>Alabama</td><td>Fayette County</td><td>16302</td></tr><tr><th>30</th><td>01059</td><td>Alabama</td><td>Franklin County</td><td>31362</td></tr><tr><th>&vellip;</th><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td><td>&vellip;</td></tr></tbody></table>"
      ],
      "text/latex": [
       "\\begin{tabular}{r|cccc}\n",
       "\t& fips & state & county & population\\\\\n",
       "\t\\hline\n",
       "\t& String & String & String & Int64\\\\\n",
       "\t\\hline\n",
       "\t1 & 01001 & Alabama & Autauga County & 55869 \\\\\n",
       "\t2 & 01003 & Alabama & Baldwin County & 223234 \\\\\n",
       "\t3 & 01005 & Alabama & Barbour County & 24686 \\\\\n",
       "\t4 & 01007 & Alabama & Bibb County & 22394 \\\\\n",
       "\t5 & 01009 & Alabama & Blount County & 57826 \\\\\n",
       "\t6 & 01011 & Alabama & Bullock County & 10101 \\\\\n",
       "\t7 & 01013 & Alabama & Butler County & 19448 \\\\\n",
       "\t8 & 01015 & Alabama & Calhoun County & 113605 \\\\\n",
       "\t9 & 01017 & Alabama & Chambers County & 33254 \\\\\n",
       "\t10 & 01019 & Alabama & Cherokee County & 26196 \\\\\n",
       "\t11 & 01021 & Alabama & Chilton County & 44428 \\\\\n",
       "\t12 & 01023 & Alabama & Choctaw County & 12589 \\\\\n",
       "\t13 & 01025 & Alabama & Clarke County & 23622 \\\\\n",
       "\t14 & 01027 & Alabama & Clay County & 13235 \\\\\n",
       "\t15 & 01029 & Alabama & Cleburne County & 14910 \\\\\n",
       "\t16 & 01031 & Alabama & Coffee County & 52342 \\\\\n",
       "\t17 & 01033 & Alabama & Colbert County & 55241 \\\\\n",
       "\t18 & 01035 & Alabama & Conecuh County & 12067 \\\\\n",
       "\t19 & 01037 & Alabama & Coosa County & 10663 \\\\\n",
       "\t20 & 01039 & Alabama & Covington County & 37049 \\\\\n",
       "\t21 & 01041 & Alabama & Crenshaw County & 13772 \\\\\n",
       "\t22 & 01043 & Alabama & Cullman County & 83768 \\\\\n",
       "\t23 & 01045 & Alabama & Dale County & 49172 \\\\\n",
       "\t24 & 01047 & Alabama & Dallas County & 37196 \\\\\n",
       "\t25 & 01049 & Alabama & DeKalb County & 71513 \\\\\n",
       "\t26 & 01051 & Alabama & Elmore County & 81209 \\\\\n",
       "\t27 & 01053 & Alabama & Escambia County & 36633 \\\\\n",
       "\t28 & 01055 & Alabama & Etowah County & 102268 \\\\\n",
       "\t29 & 01057 & Alabama & Fayette County & 16302 \\\\\n",
       "\t30 & 01059 & Alabama & Franklin County & 31362 \\\\\n",
       "\t$\\dots$ & $\\dots$ & $\\dots$ & $\\dots$ & $\\dots$ \\\\\n",
       "\\end{tabular}\n"
      ],
      "text/plain": [
       "3142×4 DataFrame\n",
       "│ Row  │ fips   │ state   │ county            │ population │\n",
       "│      │ \u001b[90mString\u001b[39m │ \u001b[90mString\u001b[39m  │ \u001b[90mString\u001b[39m            │ \u001b[90mInt64\u001b[39m      │\n",
       "├──────┼────────┼─────────┼───────────────────┼────────────┤\n",
       "│ 1    │ 01001  │ Alabama │ Autauga County    │ 55869      │\n",
       "│ 2    │ 01003  │ Alabama │ Baldwin County    │ 223234     │\n",
       "│ 3    │ 01005  │ Alabama │ Barbour County    │ 24686      │\n",
       "│ 4    │ 01007  │ Alabama │ Bibb County       │ 22394      │\n",
       "│ 5    │ 01009  │ Alabama │ Blount County     │ 57826      │\n",
       "│ 6    │ 01011  │ Alabama │ Bullock County    │ 10101      │\n",
       "│ 7    │ 01013  │ Alabama │ Butler County     │ 19448      │\n",
       "│ 8    │ 01015  │ Alabama │ Calhoun County    │ 113605     │\n",
       "│ 9    │ 01017  │ Alabama │ Chambers County   │ 33254      │\n",
       "│ 10   │ 01019  │ Alabama │ Cherokee County   │ 26196      │\n",
       "⋮\n",
       "│ 3132 │ 56025  │ Wyoming │ Natrona County    │ 79858      │\n",
       "│ 3133 │ 56027  │ Wyoming │ Niobrara County   │ 2356       │\n",
       "│ 3134 │ 56029  │ Wyoming │ Park County       │ 29194      │\n",
       "│ 3135 │ 56031  │ Wyoming │ Platte County     │ 8393       │\n",
       "│ 3136 │ 56033  │ Wyoming │ Sheridan County   │ 30485      │\n",
       "│ 3137 │ 56035  │ Wyoming │ Sublette County   │ 9831       │\n",
       "│ 3138 │ 56037  │ Wyoming │ Sweetwater County │ 42343      │\n",
       "│ 3139 │ 56039  │ Wyoming │ Teton County      │ 23464      │\n",
       "│ 3140 │ 56041  │ Wyoming │ Uinta County      │ 20226      │\n",
       "│ 3141 │ 56043  │ Wyoming │ Washakie County   │ 7805       │\n",
       "│ 3142 │ 56045  │ Wyoming │ Weston County     │ 6927       │"
      ]
     },
     "execution_count": 18,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "get_county_populations()"
   ]
  }
 ],
 "metadata": {
  "@webio": {
   "lastCommId": null,
   "lastKernelId": null
  },
  "kernelspec": {
   "display_name": "Julia 1.4.1",
   "language": "julia",
   "name": "julia-1.4"
  },
  "language_info": {
   "file_extension": ".jl",
   "mimetype": "application/julia",
   "name": "julia",
   "version": "1.4.1"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
